# Documentation
Here you can learn how to use this module.

Note: The discord api updates the commands every hour, if you want your command to be seen before just eject and install your bot back to your server.

Note: This command is oriented to discord.js so it is recommended that you have it installed.

Note: All methods and events in the module are recommended to be placed in the bot's ready event, because if the client is not ready, the module is quite prone to failure (except for classes and their methods, they do not need it).

Note: Remember to invite your bot with the oauth guilds.commands, if you don't do this, slash commands won't work.

# Classes


## SlashBaseModule()

### Properties

data: This property stores the data as it will be sent to the discord api.

### Methods

setName(string Name): Sets the command name.

setDescription(string Description): Sets the command description.




## SlashMessage()

### Properties

interaction: The interaction returned by the discord api.

member: this is the interaction returned by the discord api.

name: The command name.

id: the interaction id.

createdAt: this is the interaction returned by the discord api.

client: the client who received the command.

options: returns an array containing the options that were chosen or specified by the user.

### Methods

reply(string message): responds to the command.



## SlashCommand(guildId [Optional]) extended from SlashBaseModule

### Properties

data.options: Here are stored the options that the command will have.

guildId: This is the id of the server for which the command was created, in case no server is specified, the command will be global and this property will be undefined.

### Methods

addOption(class slashOption): An option is added to the command.




## slashOption() extended from SlashBaseModule

### Properties

data.choices: Here are stored the choices that are added.

data.type: Here you specify the type of option that will be this, 

### Methods

setType(string type): Sets the option type, these are the types availables: subCommand, subCommandGroup, string, integer, boolean, user, channel, role.

isRequired(bool enabled): Make this option a obligatory option.

addChoice(string name, string value): A choice is added to the option.




# Module Methods

<promise> post(client Client): With this method you create or update the commands created.

getPostedCommands(client Client, snowflake guildId [Optional]): returns an array with all the commands created and usable for the user.

removeCommand(client Client, snowflake id, snowflake guildId [Optional]): deletes a command already created using its id, it can be obtained with the getPostedCommands method.

# Module Events

onSlashCommand(client, function): returns a slashMessage each time a command is used.

# Examples

```javascript
const Discord = require('discord.js');
const client = new Discord.Client();

const slashManager = require('slash-command-discord.js'); 

client.login(process.env.token)

const test = new slashManager.command() // creating a new command

test.setName("My first command") // setting the command name
test.setDescription("This is my first slash command.") // setting the command description

client.on('ready', () => {

     slashManager.onSlashCommand(client, (command, interaction) => { // a listener for every time a command is used
    
         console.log(command);

         command.reply(`Used command: ` + command.name); // respond to the user

    })

    slashManager.post(client); // Posting the command, to make it visible on all servers

})
```
