<h1>Acceptation Criteria Tests

<h2>Table of Contents</h2>

- [Introduction](#introduction)
- [Testing Acceptation Criteria](#testing-acceptation-criteria)
  - [Tournament data can be filled in from the frontend](#tournament-data-can-be-filled-in-from-the-frontend)
  - [Tournament data can be stored in the tournament database](#tournament-data-can-be-stored-in-the-tournament-database)
- [Automatic Testing](#automatic-testing)
- [Summary](#summary)

# Introduction

In this document, I will show how I have tested functionality that is relevant to common user interactions with my application. In the ['Code Flow According to Acceptation Criteria' document](/Proof/Web%20Application/Code%20Flow%20According%20to%20Acceptation%20Criteria.md), I have analyzed a user story and shown what its acceptation criteria are. The goal of this document is to prove that all of the mentioned acceptation criteria are tested.

# Testing Acceptation Criteria

The acceptation criteria that need to be tested, are the following:

- *Tournament data can be filled in from the frontend.*
- *Tournament data can be sent to the tournament service through a POST request.*
- *Tournament data can be retrieved from the tournament service through a GET request.* 
- *Tournament data can be shown on the frontend.*
- *Tournament data can be stored in the tournament database.*
- *Tournament data can be rejected if the data is not valid.*

I will be showing how I have tested two of those criteria. One criterion is relevant for the frontend, and the other for the backend. For the full analysis of these acceptation criteria and how I have implemented them, go to the ['Code Flow According to Acceptation Criteria' document](/Proof/Web%20Application/Code%20Flow%20According%20to%20Acceptation%20Criteria.md).

## Tournament data can be filled in from the frontend

The code in `CreateTournament.vue` belongs to this acceptation criterion, and needs to be tested.

This is its code:

```javascript
<template>
    <p>Create a new tournament:</p>
    <input v-model="name" placeholder="name"/>
    <input v-model="maxRounds" placeholder="max rounds"/>
    <input v-model="timePerPlayer" placeholder="time per player"/>
    <button class="button__login" @click="createTournament(name, maxRounds, timePerPlayer)">Create</button>
</template>

<script>  
import {  v4 as uuidv4 } from 'uuid';
import { createTournament } from '@/services/TournamentService';

export default {
    name: "TournamentList",
    data() {
    return {
        hostId: uuidv4(),
        name: '',
        status: 'PLANNED',
        startTime: '2025-06-11T16:00:00.000Z',
        maxRounds: '',
        timePerPlayer: ''
    }
    },
    methods: {
        async createTournament(name, maxRounds, timePerPlayer) {
            const tournament = {
                hostId: this.hostId,
                name: name,
                status: this.status,
                startTime: this.startTime,
                maxRounds: maxRounds,
                timePerPlayer: timePerPlayer
            }

            await createTournament(tournament)
            .then(function (response) {
                window.location.reload()
            })
        }
    }
};
</script>
```

The test in `CreateTournament.test.js` is relevant to the acceptation criterion:

```js
import CreateTournament from '@/components/CreateTournament.vue'
import { mount } from '@vue/test-utils'

describe('Create Tournament', () => {

    test('creates a tournament', async () => {
        const createSpy = vi.spyOn(CreateTournament.methods, 'createTournament')

        const wrapper = mount(CreateTournament, {
            data() {
                return {
                    name: 'test name',
                    maxRounds: '5',
                    timePerPlayer: '20'
                }
            }
        })

        await wrapper.find('button').trigger('click')

        expect(createSpy).toHaveBeenCalledTimes(1)
        expect(createSpy).toHaveBeenCalledWith('test name', '5', '20')
    })
})
```

I am mocking the `createTournament` method in `CreateTournament.vue` with `vitest` (`vi`) and keeping an eye on what happens to that method by creating a spy.

```js
const createSpy = vi.spyOn(CreateTournament.methods, 'createTournament')
```

Then, I am creating an instance of the component and putting it in a vue-wrapper. I pass in the values which are normally inputted by the application user.

```js
        const wrapper = mount(CreateTournament, {
            data() {
                return {
                    name: 'test name',
                    maxRounds: '5',
                    timePerPlayer: '20'
                }
            }
        })
```

After that, I am firing the `click` event by simulating a button click by the user. This action should cause the `createTournament()` method to be executed.

```js
await wrapper.find('button').trigger('click')
```

I then check through the spy whether the method was truly called and whether the correct data was passed in.

```js
expect(createSpy).toHaveBeenCalledTimes(1)
expect(createSpy).toHaveBeenCalledWith('test name', '5', '20')
```

## Tournament data can be stored in the tournament database

The code that should be tested for this criterion is present in `TournamentService.java` and `TournamentController.java`.

**TournamentService.java**

```java
public void addNewTournament(Tournament tournament) {
    tournamentRepository.save(tournament);
}
```

**TournamentController.java**

```java
@PostMapping
public ResponseEntity<Tournament> addTournament(@RequestBody RequestModel requestModel) {
    Tournament tournament = convertToEntity(requestModel);

    String message = tournamentService.tournamentValidation(tournament);
    if (!message.isEmpty()) {
        throw new ResponseStatusException(
                HttpStatus.BAD_REQUEST,
                message
        );
    }

    tournamentService.addNewTournament(tournament);
    Optional<Tournament> returnedTournament = tournamentService.getTournament(tournament.getId());
    if (returnedTournament.isEmpty()) {
        throw new ResponseStatusException(
                HttpStatus.INTERNAL_SERVER_ERROR,
                "The tournament was not added successfully. Ask the developers to fix this issue."
        );
    }
    return new ResponseEntity<>(returnedTournament.get(), HttpStatus.CREATED);
}
```

The `addTournament()` function in the controller calls the `addNewTournament()` function in the service. It also calls other service funtions, but those will not be tested for this criterion. Those belong to other criteria and have tests which belong to those other criteria. They will not be shown in this document.

These tests in `TournamentServiceTest.java` and `TournamentControllerTest.java` are relevant to this acceptation criterion:

**TournamentServiceTest.java**

```java
    @Test
    void AddsANewTournament() {
        // Arrange
        Tournament tournament = tournamentData.getTournaments().get(0);
        // Act
        tournamentService.addNewTournament(tournament);
        // Assert
        verify(tournamentRepository).save(tournament);
    }
```

**TournamentControllerTest.java**

```java
void AddsANewTournament() throws Exception {

    // Arrange
    RequestModel requestModel = new RequestModel(
            tournament.getHostId(),
            tournament.getName(),
            tournament.getStartTime(),
            tournament.getMaxRounds(),
            tournament.getTimePerPlayer()
    );

    // Act & Assert
    when(tournamentService.tournamentValidation(isA(Tournament.class))).thenReturn("");
    when(tournamentService.getTournament(isA(UUID.class))).thenReturn(Optional.of(tournament));

    mockMvc.perform(post("/tournament/")
                .content(objectMapper.writeValueAsString(requestModel))
                .contentType(MediaType.APPLICATION_JSON))
            .andDo(print())
            .andExpect(status().isCreated())
            .andExpect(content().contentType(MediaType.APPLICATION_JSON))
            .andExpect(jsonPath("$.id", is(tournament.getId().toString())))
            .andExpect(jsonPath("$.hostId", is(tournament.getHostId().toString())))
            .andExpect(jsonPath("$.name", is(tournament.getName())))
            .andExpect(jsonPath("$.status", is(tournament.getStatus().toString())))
            .andExpect(jsonPath("$.startTime", is(tournament.getStartTime().format(dateTimeFormatter))))
            .andExpect(jsonPath("$.finishTime", is(tournament.getFinishTime().format(dateTimeFormatter))))
            .andExpect(jsonPath("$.currentRound", is(tournament.getCurrentRound())))
            .andExpect(jsonPath("$.maxRounds", is(tournament.getMaxRounds())))
            .andExpect(jsonPath("$.timePerPlayer", is(tournament.getTimePerPlayer())))
            .andExpect(jsonPath("$.createdAt", is(tournament.getCreatedAt().format(dateTimeFormatter))))
            .andExpect(jsonPath("$").isNotEmpty());

    verify(tournamentService).tournamentValidation(isA(Tournament.class));
    verify(tournamentService).addNewTournament(isA(Tournament.class));
    verify(tournamentService).getTournament(isA(UUID.class));
}
```
I am testing them using the `spring-boot-starter-test` dependency, which has JUnit5 and mockito.

The test in `TournamentServiceTest.java` is very straightforward.

In here, test data is being loaded from the `getTournaments()` method in `TournamentData.java`. It specifically retrieves one tournament.

```java
Tournament tournament = tournamentData.getTournaments().get(0);
```

After that, the tournament is being passed to the `addNewTournament()` method in the tournament service. It does not actually save a tournament, because the `tournamentRepository` in the service is being mocked.

```java
tournamentService.addNewTournament(tournament);
```

Finally, mockito will check if the mocked repository called the `save()` method. If that is the case, the test will succeed.

```java
verify(tournamentRepository).save(tournament);
```

The test in `TournamentControllerTest.java` is a bit more complicated.

First, a valid request model is created, using data from a tournament which is present in `TournamentData.java`.

```java
RequestModel requestModel = new RequestModel(
        tournament.getHostId(),
        tournament.getName(),
        tournament.getStartTime(),
        tournament.getMaxRounds(),
        tournament.getTimePerPlayer()
);
```

Then, some preparations are made for when certain methods are called that shouldn't be tested in this test.

```java
when(tournamentService.tournamentValidation(isA(Tournament.class))).thenReturn("");
when(tournamentService.getTournament(isA(UUID.class))).thenReturn(Optional.of(tournament));
```

After that, a fake POST request is made using MockMVC. Many assertions are made to make sure that the response returns the right data.

```java
mockMvc.perform(post("/tournament/")
            .content(objectMapper.writeValueAsString(requestModel))
            .contentType(MediaType.APPLICATION_JSON))
        .andDo(print())
        .andExpect(status().isCreated())
        .andExpect(content().contentType(MediaType.APPLICATION_JSON))
        .andExpect(jsonPath("$.id", is(tournament.getId().toString())))
        .andExpect(jsonPath("$.hostId", is(tournament.getHostId().toString())))
        .andExpect(jsonPath("$.name", is(tournament.getName())))
        .andExpect(jsonPath("$.status", is(tournament.getStatus().toString())))
        .andExpect(jsonPath("$.startTime", is(tournament.getStartTime().format(dateTimeFormatter))))
        .andExpect(jsonPath("$.finishTime", is(tournament.getFinishTime().format(dateTimeFormatter))))
        .andExpect(jsonPath("$.currentRound", is(tournament.getCurrentRound())))
        .andExpect(jsonPath("$.maxRounds", is(tournament.getMaxRounds())))
        .andExpect(jsonPath("$.timePerPlayer", is(tournament.getTimePerPlayer())))
        .andExpect(jsonPath("$.createdAt", is(tournament.getCreatedAt().format(dateTimeFormatter))))
        .andExpect(jsonPath("$").isNotEmpty());
```

Lastly, some assertions are made to see if the methods from the tournament service have been passed in the correct data.

```java
verify(tournamentService).tournamentValidation(isA(Tournament.class));
verify(tournamentService).addNewTournament(isA(Tournament.class));
verify(tournamentService).getTournament(isA(UUID.class));
```

# Automatic Testing

All the components in the Chess Tournament Manager have a working CI pipeline, which automatically tests the relevant application when a push to GitHub has occured and when the code is present in a pull request. For more information about how the CI pipelines work, go [here](/Proof/CI%20and%20CD/Project%20Workflows.md).

# Summary

I have shown several acceptation criteria and explained how I tested two of them using vitest, vue-test-utils and spring-boot-starter-test.