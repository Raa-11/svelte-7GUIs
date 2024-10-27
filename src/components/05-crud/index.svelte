<script lang="ts">
    type Person = {
        name: string
        country: string
    }

    let people = $state([
        { name: 'Seno', country: 'Indonesia' },
        { name: 'Rama', country: 'Indonesia' },
        { name: 'Dhani', country: 'Indonesia' },
    ])

    let selected = $state<Person>()
    let person = $state({ name: '', country: '' })
    let prefix = $state('')
    const filteredPeople = $derived(
        prefix ? people.filter((p) => p.country.toLocaleLowerCase().startsWith(prefix)) : people,
    )

    $effect(() => {
        person = {
            name: selected?.name ?? '',
            country: selected?.country ?? '',
        }
    })

    function createPerson() {
        people.push(person)
        clearFields()
    }

    function updatePerson() {
        const index = people.indexOf(selected!)
        people[index] = { name: person.name, country: person.country }
    }

    function deletePerson() {
        people = people.filter((p) => p.name !== person.name || p.country !== person.country)
        clearFields()
    }

    function clearFields() {
        person = { name: '', country: '' }
    }
</script>

<div class="container surface-2">
    <div class="search">
        <label class="group">
            <span>Filter prefix:</span>
            <input type="text" bind:value={prefix} />
        </label>
    </div>

    <label class="people">
        <span class="sr-only">Names:</span>
        <select bind:value={selected} size="5">
            {#each filteredPeople as person}
                <option value={person}>{person.country}, {person.name}</option>
            {/each}
        </select>
    </label>

    <div class="details">
        <label class="group">
            <span>Name:</span>
            <input type="text" bind:value={person.name}/>
        </label>

        <label class="group">
            <span>Country:</span>
            <input type="text" bind:value={person.country} />
        </label>
    </div>

    <div class="actions space-x">
        <button class="create" onclick={createPerson}>Create</button>
        <button class="update" onclick={updatePerson}>Update</button>
        <button class="delete" onclick={deletePerson}>Delete</button>
    </div>
</div>

<style>
	.container {
		width: 500px;
		display: grid;
		grid-template-areas:
			'search .'
			'people details'
			'actions actions';
		grid-template-columns: 240px 1fr;
		grid-auto-rows: auto;
		gap: var(--size-3);
		padding: var(--size-3);

        option {
            color: black;
        }

		.search {
			grid-area: search;

			.group {
				display: grid;
				grid-template-columns: 2fr 1fr;
				align-items: baseline;
			}
		}

        input[type="text"] {
            color: black;
        }

		.people {
			grid-area: people;
		}

		.details {
			grid-area: details;
			display: grid;
			grid-template-columns: auto 1fr;
			grid-template-rows: repeat(2, auto) 1fr;
			align-items: baseline;
			gap: var(--size-2);

			.group {
				display: contents;
			}
		}

        .create {
            color: green;
        }

        .update {
            color: rgb(209, 209, 0);
        }

        .delete {
            color: red;
        }

		.actions {
			grid-area: actions;
		}
	}
</style>