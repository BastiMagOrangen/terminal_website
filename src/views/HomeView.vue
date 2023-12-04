<script setup>
import ShowCommands from '../components/ShowCommands.vue';
</script>

<template>
  <div v-for="command1 in commandLog">
    <ShowCommands :content=command1 />
  </div>
  <div class="terminal">
    <div class="begin">
      <p>{{ name }}</p>
    </div>
    <div class="end">
      <input v-model="command" :type="type" autofocus v-on:keyup.enter="enterCommand()" v-on:keyup.up="lastCommand()" v-on:keyup.down="recentCommand()" spellcheck="false">
    </div>
    
  </div>
</template>

<script>

export default {
  data() {
    return {
      type: "text",
      name: "guest@basti:~$",
      password: "basti",
      commands: new Map(),
      command: "",
      pastCommands: [],
      position: 0,
      commandLog: []
    }
  },
  methods: {
    enterCommand() {
      console.log(this.command)
      this.pastCommands.push(this.command)
      this.position = this.pastCommands.length
      this.startCommand(this.command.toLocaleLowerCase())
    },
    startCommand(cmd) {
      var entered_command = this.command
      this.command = ""
      if(this.name == "password:" && cmd == this.password) {
        this.name = "root@basti:~$"
        this.type = "text"
        entered_command = ""
        return
      }
      else if(this.name == "password:") {
        this.name = "guest@basti:~$"
        this.type = "text"
        entered_command = ""
        return
      }
      this.PushCommandLine(entered_command)
      cmd = cmd.replace(" ", "")
      switch(cmd) {
        case "":
          break
        case "social":
          var text = `<div style='margin-left: 20px; margin-top: 20px; margin-bottom: 20px;'><p><span>Github: https://github.com/BastiMagOrangen</span></p></div>`
          this.commandLog.push(text)
          break
        case "login":
          this.name = "password:"
          this.type = "password"
          break
        case "social-github":
        case "social-git":
        case "social-g":
          var text = `<div style='margin-left: 20px; margin-top: 20px; margin-bottom: 20px;'><p><span>Github: https://github.com/BastiMagOrangen</span></p></div>`
          this.commandLog.push(text)
          window.open("https://github.com/BastiMagOrangen", "_blank")
          break
        case "help":
          var text = `<div style='margin-left: 20px; margin-top: 20px; margin-bottom: 20px;'>`
          console.log(text)
          this.commands.forEach((value, key) => {
            console.log(key, value)
            text += `<p><span class='highlight'>${key}</span><span> ${value}</span></p>`
          })
          console.log(text)
          text += `</div>`
          console.log(text)
          this.commandLog.push(text)
          break
        case "secret":
          window.open("https://www.youtube.com/watch?v=dQw4w9WgXcQ", "_blank")
          break
        case "clear":
          this.commandLog = []
          break
        default:
          var text = `<div><p style='color: red !important;'><span>Command </span><span class='highlight'>'${entered_command}' </span><span> not found. Type </span><span class='highlight'>'help' </span><span>to list all commands</span></p></div>`
          this.commandLog.push(text)
          break
      }
    },
    lastCommand() {
      if(this.position != 0) {
        this.position -= 1
        if(this.pastCommands[this.position] != "") {
          this.command = this.pastCommands[this.position]
        }
      }
    },
    recentCommand() {
      if(this.position != this.pastCommands.length) {
        this.position += 1
        if(this.pastCommands[this.position] === undefined) {
          this.command = ""
        } else {
          this.command = this.pastCommands[this.position]
        }
      }
    },
    PushCommandLine(command) {
      this.commandLog.push(`<style>.terminal{
  display: flex;
  gap: 10px;
}
.begin p{
  color: #4E9A06;
  margin: 0;
  padding: 0;
  background: none;
  border: none;
  border-radius: 0;
}
.end input{
  color: azure;
  outline: none;
  -webkit-appearance: none;
  -moz-appearance: none;
	appearance: none;
  padding: 0;
  background: none;
  border: none;
  border-radius: 0;
  width: 100%;
}
.end {
  width: 100%;
}
p{
  color: burlywood;
}</style></div><div class="terminal"><div class="begin"><p>${this.name}</p></div><div class="end">
      <input v-model="command" disabled spellcheck="false" value="${command}">
    </div></div>`)
    }
  },
  mounted() {
    this.commands.set("secret", "Bitte nicht starten")
    this.commands.set("help", "List all commands")
    this.commands.set("clear", "Clear Terminal")
    this.commands.set("social", "View Social Accounts")
    this.commands.set("login", "Login into Admin Account")
    console.log(this.commands)
  }
}

</script>

<style scoped>
.terminal{
  display: flex;
  gap: 10px;
}
.begin p{
  color: #4E9A06;
  margin: 0;
  padding: 0;
  background: none;
  border: none;
  border-radius: 0;
}
.end input{
  color: azure;
  outline: none;
  -webkit-appearance: none;
  -moz-appearance: none;
	appearance: none;
  padding: 0;
  background: none;
  border: none;
  border-radius: 0;
  width: 100%;
}
.end {
  width: 100%;
}
</style>