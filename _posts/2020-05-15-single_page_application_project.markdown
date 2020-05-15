---
layout: post
title:      "Single Page Application Project"
date:       2020-05-15 22:37:57 +0000
permalink:  single_page_application_project
---


The fourth project for Flatiron is a single page application with a rails backend and an object oriented javascript and HTML frontend.  My project is a Dungeons and Dragons character generator, using the rules of the Dungeons and Dragons handbook to generate ability scores and modifiers, along with other class/race/background specific information.  

I found this very nice D&D character form online that I used as the "read" and "update" part of the CRUD actions for a new character: https://codepen.io/anon/pen/dWKdvm/

My character class inherits from an original class of UniversalCharacter that looks like this: 
```class UniversalCharacter {
    constructor() {
      this.dexterity = this.getAbilityScore()
      this.constitution = this.getAbilityScore()
      this.wisdom = this.getAbilityScore()
      this.intellect = this.getAbilityScore()
      this.charisma = this.getAbilityScore()
      this.strength = this.getAbilityScore()
      // half elf has 2 extra ability points to spend wherever you want... make this its own function
      this.free_ability_pts = 0
      this.speed = 25
      this.hp = 0
      this.alignment= "";
      this.language= ["Common"];
      this.proficiencies = [];
      // these are for editing for people who want to save this stuff to DB
      this.personality_traits = "";
      this.ideals = "";
      this.bonds = "";
      this.flaws = "";
      this.features_and_traits = "";
      this.equipment = "";
      this.attacks_and_spells = "";
      this.background = "";
      this.saving_throws = []
  
    }
  // roll 4 six-sided dice, add the top 3 numbers.
    getAbilityScore(){
      let arr = [Math.floor(Math.random()*6+1), Math.floor(Math.random()*6+1), Math.floor(Math.random()*6+1), Math.floor(Math.random()*6+1)].sort();
      let arr1 = arr.slice(0,3);
      return arr1.reduce((total, element) => {return total + element}, 0)
    }
    // calculate ability modifier
    // why is this not avail on an instance of a character?  char.modifier(10) method not defined
    modifier(value) {
      return Math.floor((value - 10) / 2)
    }
  }
  ```
	
	The Race class inherits from the UniversalCharacter class:
	```
class Race extends UniversalCharacter {
    constructor(race) {
      super()
      this.race = race
      this.selectRaceModifiers()
    }
  
    selectRaceModifiers(){
      // console.log('in race modifier ' + this.hp);
      switch (this.race) {
        case 'Dwarf':
          this.constitution += 2;
          this.hp += 1;
          this.alignment += "Lawful";
          this.proficiencies = this.proficiencies.push("History");
          // console.log('hp under race class is' + this.hp);
          break;
        case 'Elf':
          this.dexterity += 2;
          this.speed += 5;
          this.language = this.language.push("Elvish");
          this.alignment += "Chaotic G/E";
          this.proficiencies = this.proficiencies.push("Perception");
          break;
        case 'Halfling':
          this.language = this.language.push("Halfling");
          this.alignment += "Lawful Good";
          this.dexterity += 2;
          break;
        case 'Human':
          this.language = this.language.push("Any one other");
          this.alignment += "any";
          this.dexterity += 1;
          this.wisdom += 1;
          this.intellect += 1;
          this.charisma += 1;
          this.strength += 1;
          this.constitution += 1;
          this.speed += 5;
          break;
        case 'Dragonborn':
          this.language = this.language.push("Draconic");
          this.alignment = "Chaotic G/E";
          this.strength += 2;
          this.charisma += 1;
          this.speed += 5;
          break;
        case 'Gnome':
          this.language = this.language.push("Gnomish");
          this.alignment = "Neutral Good";
          this.intellect += 2;
          break;
        case 'Half-Elf':
          this.language = this.language.push("Elvish", "one more");
          this.proficiencies = this.proficiencies.push("any two");
          this.free_ability_pts += 2;
          this.charisma += 2;
          this.speed += 5;
          break;
        case 'Half-Orc':
          this.language = this.language.push("Orcish");
          this.proficiencies = this.proficiencies.push("Intimidation");
          this.strength += 1;
          this.constitution += 1;
          this.speed += 5;
          break;
        case 'Tiefling':
          this.alignment += "Chaotic Evil";
          this.language = this.language.push("Infernal");
          this.intellect += 1;
          this.charisma += 2;
          this.speed += 5;
          break;
      }
    }
  }
  ```
	The CharClass inherits from the race class:
	```
	
class CharClass extends Race {
    constructor(race, charClass) {
      super(race)
      this.charClass = charClass
      this.selectClassModifiers()
    }
    selectClassModifiers(){
      // if(this.charClass == "Paladin") {
      //   this.hitDice = "1d10"
      //   this.hp = 10 + this.modifier(this.constitution)
      // }
      switch (this.charClass) {
        case 'Barbarian':
          this.hitDice = "1d12";
          this.hp += Math.floor(Math.random()*12+1) + this.modifier(this.constitution);
          this.saving_throws.push("Strength", "Constitution");
          // console.log(`hp under class is ${this.hp}`);
          break;
        case 'Bard':
          this.hitDice = "1d8";
          this.hp += Math.floor(Math.random()*8+1) + this.modifier(this.constitution);
          this.saving_throws.push("Dexterity", "Charisma");
          break;
        case 'Cleric':
          this.hitDice = "1d8";
          this.hp += Math.floor(Math.random()*8+1) + this.modifier(this.constitution);
          this.saving_throws.push("Wisdom", "Charisma");
          break;
        case 'Druid':
          this.hitDice = "1d8";
          this.hp += Math.floor(Math.random()*8+1) + this.modifier(this.constitution);
          this.saving_throws.push("Intellect", "Wisdom");
          break;
        case 'Fighter':
          this.hitDice = "1d10";
          this.hp += Math.floor(Math.random()*10+1) + this.modifier(this.constitution);
          this.saving_throws.push("Strength", "Constitution");
          break;
        case 'Monk':
          this.hitDice = "1d8";
          this.hp += Math.floor(Math.random()*8+1) + this.modifier(this.constitution);
          this.saving_throws.push("Strength", "Dexterity");
          break;
        case 'Paladin':
          this.hitDice = "1d10";
          this.hp += Math.floor(Math.random()*10+1) + this.modifier(this.constitution);
          this.saving_throws.push("Wisdom", "Charisma");
          break;
        case 'Ranger':
          this.hitDice = "1d10";
          this.hp += Math.floor(Math.random()*10+1) + this.modifier(this.constitution);
          this.saving_throws.push("Strength", "Dexterity");
          break;
        case 'Rogue':
          this.hitDice = "1d8";
          this.hp += Math.floor(Math.random()*8+1) + this.modifier(this.constitution);
          this.saving_throws.push("Dexterity", "Intellect");
          break;
        case 'Sorcerer':
          this.hitDice = "1d6";
          this.hp += Math.floor(Math.random()*6+1) + this.modifier(this.constitution);
          this.saving_throws.push("Charisma", "Constitution");
          break;
        case 'Warlock':
          this.hitDice = "1d8";
          this.hp += Math.floor(Math.random()*8+1) + this.modifier(this.constitution);
          this.saving_throws.push("Wisdom", "Charisma");
          break;
        case 'Wizard':
          this.hitDice = "1d6";
          this.hp += Math.floor(Math.random()*6+1) + this.modifier(this.constitution);
          this.saving_throws.push("Intellect", "Wisdom");
          break;
      }
    }
  }
  ```
	and the Background class inherits from the race class, and finally the Character class inherits from the background class:
	```
class Character extends Background {
  constructor(name, race, charClass, background, player, id) {
    super(race, charClass, background)
    this.name = name
    this.id = id
    this.player = player
  }
	}
	```
	
	The ability scores follow the D&D handbook where you roll four 6-sided dice, take the top 3 rolls and add them together, the function can be found in the UniversalCharacter Class.
	
	A Player can have many characters, so I made a list of players available to all, and the ability to create a new character using a fetch Post to the backend database. 
	
	Right now the app is a Minimal Viable Product, and I added potential to add many more features, as making a D&D character can get quite complicated, I did not implement all of the features that can be offered.  I am leaving it open to improvement later on.
	
	My biggest challenge was getting object oriented JS to be organized the way I wanted.  This MVP version of the app is not organized exactly how I would like, but it works and I can edit and organize later as I see fit.  I made many different versions of classes fought with them until ultimately deciding to get the app working and leaving it open to editing and refactoring later on.
