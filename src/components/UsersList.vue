<template>
  <div class="users-list">
    <h1>Users List</h1>

    <div>
      <label for="name"><strong>Name</strong></label>
      <input size="35px" type="text" name="name" id="name" v-model="nameInput">
    </div>

    <div>
      <label for="email"><strong>Email</strong></label>
      <input size="35px" placeholder="example@email.com" type="email" name="email" id="email" v-model="emailInput">
    </div>

    <div>
      <button type="submit" @click="push(nameInput, emailInput)">Add to List</button>
    </div>

    <div>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Email</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-bind:id="entry.lockStatus" v-for="(entry, index) of namesAndEmails" :key="entry.email">
            <td v-bind:contenteditable="entry.editable">{{ entry.name }}</td>
            <td v-bind:contenteditable="entry.editable">{{ entry.email }}</td>
            <td id="alignRight">
              <button v-bind:class="entry.buttonId" @click="toggleEditable(index)">{{ entry.buttonId === 'edit-button' ? 'Edit' : 'Confirm' }}</button>
              <button class="delete-button" @click="deleteAt(index)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
  const namesAndEmails = []

  export default {
    name: 'UsersList',
    data: () => {
      return {
        namesAndEmails
      }
    },
    methods: {
      push: (name, email) => {
        namesAndEmails.push({ name, email, editable: false, lockStatus: 'locked', buttonId: 'edit-button' })
      },
      deleteAt: (index) => {
        namesAndEmails.splice(index, 1)
      },
      toggleEditable: (index) => {
        namesAndEmails[index].editable = !namesAndEmails[index].editable
        namesAndEmails[index].lockStatus = namesAndEmails[index].lockStatus === 'locked' ? 'unlocked' : 'locked'
        namesAndEmails[index].buttonId = namesAndEmails[index].buttonId === 'edit-button' ? 'confirm-button' : 'edit-button'
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  table {
    margin-top: 50px;
    border-collapse: collapse;
    width: 100%;
  }
  div {
    margin-top: 25px;
    margin-bottom: 5px;
  }
  input {
    width: 100%;
    display: block;
    padding: 12px 10px;
    margin: 5px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }
  tr {
    height: 10px;
    border-bottom: 1px solid #ccc;
  }
  th {
    text-align: left;
  }
  td {
    padding-top: 5px;
    padding-bottom: 5px;
  }
  button {
    color: white;
    background-color: rgb(58, 158, 58);
    border: 10px;
    border-color: black;
    border-radius: 5%;
    cursor: pointer;
    padding: 8px 15px;
    margin-right: 5px;
    transition: .3s;
  }
  button:hover{
    background: rgb(44, 116, 44);
    color: white;
  }
  #locked {
    background-color: rgb(228, 228, 228);
  }
  #unlocked {
    background-color: white;
  }
  #alignRight {
    text-align: right;
  }
  .delete-button {
    background-color: rgb(228, 84, 79);
  }
  .edit-button {
    background-color: rgb(118, 182, 255);
  }
  .confirm-button {
    background-color: rgb(58, 158, 58);
  }
  .confirm-button:hover {
    background-color: rgb(44, 116, 44);
  }
  .edit-button:hover {
    background-color: rgb(91, 146, 207);
  }
  .delete-button:hover {
    background-color: rgb(182, 58, 54);
  }
</style>
