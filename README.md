# Slack RPG Official Add-on
[![Build Status](https://travis-ci.org/slack-rpg/addon-official.svg)](https://travis-ci.org/slack-rpg/addon-official)

Official add-on pack for [Slack RPG](https://github.com/slack-rpg/slack-rpg)

Add-on packs are folders containing JSON files with new locations names, monsters, etc. Each folder acts as a namespace, with the name of the user/repo as the top level namespace.

# TOC
<!-- TOC depthFrom:2 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Creating your own Add-on](#creating-your-own-add-on)
- [Validating your Add-on](#validating-your-add-on)
- [Add-on Formats](#add-on-formats)
	- [Global](#global)
	- [Locations](#locations)
		- [Names](#names)
		- [Descriptions](#descriptions)
		- [Adjectives](#adjectives)
	- [Monsters](#monsters)
	- [Names](#names)
	- [Weapons](#weapons)
		- [Types](#types)
		- [Weapons](#weapons)

<!-- /TOC -->

## Creating your own Add-on
If you want to create your own add-on to include in [Slack RPG](slack-rpg/slack-rpg), the fastest way is to for this repository and either add a new folder or modify the files in the default folder.

## Validating your Add-on
We have provided a script to validate your add-on to be sure it follows the format expected.
1. Install required modules using `npm install`
2. Run `npm run validate` to validate your add-on:

```
$ npm run validate
default:
- locations.json is OK!
- monsters.json is OK!
- weapons.json is OK!
- names.json is OK!
```

## Add-on Formats
### Global
All add-ons follow the same top level format:
- **type**: The type of add-on this file is for
- **version**: The version of the schema this file follows
- **data**: The actual data of your add-on

### Locations
Locations contain three types of items:

#### Names
Names consist of three arrays: pre, name, sur

Names are generated by selecting one item from each array randomly. It is then combined to form the full name. Empty strings are acceptable in pre and sur if you want the name to be short and unaltered.

Roll | pre  | name    | sur
---- | ---- | ------- | -----
1    |      | rio     |
2    |      | main    | shire
3    | dire | capital | town
4    | mme  | shanty  | ville

Given a roll of 1, 3, 4 on the table above, you would end up with a name of _Capitalville_

#### Descriptions
Descriptions is an array of short descriptions of an area. Adding the string `{{adj}}` to the description will have it replaced with a random adjective when it is built.

#### Adjectives
Adjectives is an array of adjectives to be used in a description.

Roll | adj
---- | -----
1    | funny
2    | hairy
3    | silly

Given a roll of 1 and a short description of _This is quite the {{adj}} town!_ you would end up with _This is quite the silly town!_

### Monsters
Monsters contains an array of one item type: **Monsters**!

A monster is an NPC that is hostile toward players and will attack them. They usually provide experience if they are defeated. A monster item consists of the following information:
- **id**: _string_, A unique id for the monster. It must be unique in the namespace.
- **name**: _string_, A human readable name of the monster.
- **difficulty**: _integer_, What level the player should be to fight monster. If a monster is a higher level than the player it will get bonuses for damage and attack rate. If a monster is a lower level, it will get penalties for damage and attack rate.
- **experience**: _integer_, The amount of experience a player gets for killing it
- **hitbonus**: _integer_, the bonus to hit for the monster. Positive gives greater chance to hit.
- **hitpoints**: _string_, (dice format) the amount of hit points the monster gets
- **damage**: _string_, (dice format) the amount of damage its attack does
- **attacks**: _string[]_, A list of verbs that describe its attack

### Names
Names are used to generate names of NPCs and consists of three arrays: pre, name, sur

Names are generated by selecting one item from each array randomly. It is then combined to form the full name. Empty strings are acceptable in pre and sur if you want the name to be short and unaltered.

Roll | pre | name  | sur
---- | --- | ----- | -------
1    |     | bob   |
2    |     | jim   | todd
3    | sir | mary  | frank
4    | mme | billy | muffins

Given a roll of 1, 3, 4 on the table above, you would end up with a name of _Marymuffins_

### Weapons
Weapons are used by characters to attack.

#### Types
Types is an array of Weapon Types. Weapon types are generic types of weapons and provides verbs for actions.
- **id**: _string_, A unique id for the weapon type. It must be unique in the namespace.
- **phrases**: _object_
  - **attack**: _string[]_, an array of verbs that describe how weapons of that type attack
  - **break**: _string[]_, an array of verbs that describe how weapons of that type break

#### Weapons
Weapons is an array of Weapons.
- **id**: _string_, A unique id for the weapon. It must be unique in the namespace.
- **name**: _string_, A human readable name of the weapon.
- **type**: _string_, The ID of weapon type
- **hands**: _integer_, (1,2) The number of hands needed to wield the weapon
- **damage**: _string_, (dice format) the amount of damage the weapon does
- **rarity**: _integer_, How rare the item is, calculate as the ratio of 1:N
- **fragility**: _integer_, How likely the weapon is to break.
- **wear**: _integer_, how many uses before it gets a wear point.
