<script>
  let users = [
    { id: 1, name: "Javier Ruiz", email: "javier@ruiz.com" },
    { id: 2, name: "Manolito Gomez", email: "manolito@gomez.com" },
  ];
  
  let newUser = { name: "", email: "" };
  let filterName = "";

  function addUser (){
    if (newUser.name && newUser.email) {
      const newUserId = Date.now();
      users = [...users, {
        id: newUserId,
        name: newUser.name,
        email: newUser.email,
      }];
      newUser.name = "";
      newUser.email = "";
    }
  };
  
  function removeUser (userId){
    users = users.filter(user => user.id !== userId);
  };

  $: filteredUsers = users.filter(user => user.name.toLowerCase().includes(filterName.toLowerCase()));
</script>

<h1>Lista de usuarios en svelte</h1>
<input type="text" bind:value={filterName} placeholder="Filtrar por nombre">
<ul>
  {#each filteredUsers as user (user.id)}
    <li>
      {user.name} - {user.email}
      <button on:click={() => removeUser(user.id)}>Eliminar</button>
    </li>
  {/each}
</ul>
<div class="user-form">
  <input type="text" bind:value={newUser.name} placeholder="Nombre">
  <input type="email" bind:value={newUser.email} placeholder="Correo electrónico">
  <button on:click={addUser}>Agregar Usuario</button>
</div>

<style>
  .user-form {
    margin-top: 20px;
    display: flex;
    gap: 10px;
  }

  input[type="text"],
  input[type="email"] {
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }

  button {
    padding: 5px 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
  }
</style>
