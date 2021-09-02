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

Install required dependencie:
```sh-session
npm install discord.js
```

here is an example of a simple bot with a menu:
```js
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
    menu.on("collectorEnd", () => console.log("finished the menu collector"));
  }
});

client.login("TOKEN");

```

### if you have anything you want to add you can contribute on [github](https://github.com/arturoAtomplay/easymenu-pages)
