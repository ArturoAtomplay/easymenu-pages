# easymenu-pages
> this module is inspired and with a large part of the code of [discord.js-menu](https://github.com/jowsey/discord.js-menu)
## About
module that helps you create pages with menus, buttons and functions easily
- selectMenus
- buttons

## Installation
```sh-session
npm install easymenu-pages
```

## Example usage

Install required dependencies:
```sh-session
npm install discord.js
```

example of a menu (of course it must be in one of your commands)
```js
const EasyMenu = require("easymenu-pages");

const menu = new EasyMenu({
  channel: message.channel,
  usersID: message.author.id, //it can also be an array
  pages: [
    {
      name: "main",
      message: {
        content: "this is a easy menu",
        components: [
          new Discord.MessageActionRow().addComponents(
            new Discord.MessageSelectMenu()
              .setCustomId("select")
              .setPlaceholder("Nothing selected")
              .addOptions([
                {
                  label: "menu",
                  description: "test menu",
                  value: "toMenu",
                },
              ]),
          ),
          new Discord.MessageActionRow().addComponents(
            new Discord.MessageButton().setCustomId("delete").setLabel("delete this msg").setStyle("DANGER"),
          ),
        ],
      },
      componentsActions: {
        delete: "delete",
        toMenu: "menu",
      },
    },
    {
      name: "menu",
      message: {
        content: "Hi this is a button with function",
        components: [
          new Discord.MessageActionRow().addComponents(
            new Discord.MessageButton().setCustomId("edit").setLabel("function").setStyle("PRIMARY"),
          ),
        ],
      },
      componentsActions: {
        edit: () => {
          menu.msgMenu.edit({ content: "Wow", components: [] });
        },
      },
    },
  ],
});

menu.start();

menu.on("collectorEnd", () => console.log("Menu: finished the menu collector"));

menu.on("pageChange", (oldPage, newPage) => console.log(`Menu: page change from ${oldPage.name} to ${newPage.name}`)); //new (I think it could be useful if you know how to use it well)

```

## Changes
- add new event to menu (pageChange)

### if you have anything you want to add you can contribute on [github](https://github.com/arturoAtomplay/easymenu-pages)
