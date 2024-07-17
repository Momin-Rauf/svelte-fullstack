<script>
    export let names;

    let showModal = false;
    let currentUser = { id: null, name: '', email: '' };

    function openModal(user) {
        currentUser = user;
        showModal = true;
    }

    function closeModal() {
        showModal = false;
    }
</script>

{#if showModal}
    <div class="fixed inset-0 flex items-center z-10 justify-center bg-gray-800 bg-opacity-50">
        <div class="bg-white p-8 rounded-lg shadow-lg">
            <h2 class="text-xl font-semibold mb-4">Edit User</h2>
            <form method="POST" action="?/update">
                <input type="hidden" name="id" value={currentUser.id} />
                <div class="flex flex-wrap -mx-3 mb-2">
                    <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
                        <label
                            class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                            for="name"
                        >
                            Name
                        </label>
                        <input
                            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                            id="name"
                            type="text"
                            placeholder="Enter name"
                            name="name"
                            bind:value={currentUser.name}
                        />
                    </div>
                    <div class="w-full md:w-1/3 px-3 mb-6 md:mb-0">
                        <label
                            class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
                            for="email"
                        >
                            Email
                        </label>
                        <input
                            class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
                            id="email"
                            type="text"
                            placeholder="Enter email"
                            name="email"
                            bind:value={currentUser.email}
                        />
                    </div>
                    <button
                        type="submit"
                        class="bg-yellow-500 hover:bg-blue-700 text-white font-bold mt-5 ml-2 px-2 rounded"
                    >
                        Update User
                    </button>
                    <button
                        type="button"
                        on:click={closeModal}
                        class="bg-gray-500 text-white font-bold mt-5 ml-2 px-2 rounded"
                    >
                        Cancel
                    </button>
                </div>
            </form>
        </div>
    </div>
{/if}

<div class="mt-10 pt-10 w-full max-w-xl p-12 mx-auto rounded-lg shadow-xl dark:bg-white/10 bg-white/30 ring-1 ring-gray-900/5 backdrop-blur-lg">
    <div class="flex items-center justify-between mb-4">
        <div class="space-y-1">
            <h2 class="text-xl font-semibold">List of Users</h2>
            <p class="text-sm text-gray-500">
                Fetched {names.length} users
            </p>
        </div>
    </div>
    <div class="divide-y divide-gray-900/5">
        {#each names as user (user.id)}
            <div class="flex items-center justify-between py-3">
                <div class="flex items-center space-x-4">
                    <div class="flex">
                        <p class="font-medium pt-1 leading-none">{user.name}</p>
                        <p class="font-medium pl-5 text-gray-500 pt-0">{user.email}</p>
                    </div>
                </div>
                <form method="POST" action="/profiles?/delete">
                    <input type="hidden" name="id" id="id" value={user.id}>
                    <button type="submit">
                        <img class="w-4 float-right" src="./trash-can.svg" alt="delete" />
                    </button>
                </form>
                <button on:click={() => openModal(user)}>
                    edit
                </button>
            </div>
        {/each}
    </div>
</div>
