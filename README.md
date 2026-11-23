---Module Two Team Project Plan---

Chosen Scenario: Top Down

4 Additional Elements (Andrew):
Boss: Lord Malrick
Player Equipment Pickups: Sacred Relics
Obstacles: Traps
Enemies: Moving enemies (Lord Malrick's guard servants)

Brainstormed Concept (Cody): King's Castle
You are a loyal knight tasked with exploring King's Castle in search of six sacred relics: the Ancient Sword, Blessed Chalice, Regal Sword, Battle Standard, Enchanted Amulet, and Golden Coin Chest. 
As the player progresses through different areas of the castle, they must overcome traps, puzzles, and enemies serving the dark sorcerer Lord Malrick. 
Once all relics have been collected, the Throne Room is unlocked and the player must face Lord Malrick in a final battle. 
The game is a top-down fantasy adventure inspired by classic games such as the original Legend of Zelda and focuses on exploration, progression, relic collection, and boss encounters.

Timeline (Zach):
Follow the weekly modules as a guide to ensure that we stay on track with expected development.
Maintain status updates within our Discord communications to stay on pace.

Goals for Alpha (Ryan):
-Implement the core features for King's Castle as well as creating one or two room layouts. 

Goals for Beta (Ryan):
-Once all core features have been successfully implemented, we will take this phase to expand the world of King's Castle and its layouts. 

Communication methods:
Most, if not all, of our communications will be conducted through Discord threads. 

Meeting Schedule (Logan): 
As available through Discord threads/calls

Assigning/Reporting Methodology:
Regular check-ins and Google Docs Checklist


---Module Three QA and Testing Plan---

Testing Plan (Cody):
-Separate Play testing into two aspects: Features and Gameplay [INSERT DETAIL].

-Demo testing: Full vertical slice/market-ready build before any external presentation. 

-Code Release: Final checklist against our test plan/stability - Late production

Example checklist items (Zach):
- Game launches
- Saving/loading
- Pause menu/settings
- Player movement/controls feel responsive/intuitive
- Combat/gameplay loop working
- Win/lose conditions
- Level can be completed from start to finish
- Collectibles/interactables work (Relics, traps, doors, etc.)
- Assets/models appear correctly
- Menus/HUD clearly displayed
- Performance works on our targeted hardware
- Progression feels intuitive
- Are rooms unique
- Are enemies and the final boss fight fair

Updating Test Plan (Andrew):
- The test plan will be updated as features or the design document are updated or changed. We will maintain documented versions of our plan and code to better track and isolate issues encountered during testing. Changes will be noted here on GitHub so everyone has easy access. We will also meet and review the plan after any milestone updates. 

Bug Reporting Plan (Ryan): 
Ultize GitHub's own Issues feature to write down issues and steps to reproduce them as well as their severity. All team members are able to report and easily update logs.

How Bugs Will Be Tracked (Logan):
-Bugs will be tracked using a central bug database where each issue is documented with its description, severity, reproduction steps, current status, and assigned team member. The team will use a status workflow to show whether bugs are new, in progress, testing, or resolved. Team members will be assigned bugs based on the area they are responsible for, and a weekly summary will be added to the project README to show the current open bugs and their progress.


---Module Four Project Log - Team Reflection---


### What parts of the testing process did the team perceive to go well?

(Zach)
Testing the UI and interaction systems in small pieces worked well.
For example, the interact prompt was tested on its own with placeholder text
before any gameplay logic was connected to it, which made layout problems easy
to separate from logic problems. Testing against a simple test pickup
(BP_TestPickup) before building more interactable types also let's make sure
everything is working before moving forward.

### How were bugs identified and corrected?

(Zach)
Bugs were found by playtesting the menus and interact as they were built and 
then tracing the cause. I used Print String nodes to confirm whether input 
events and functions were firing. Examples from the UI/UX side:
- **Interact prompt displaying incorrectly:** The prompt appeared as a solid
  white box that hid its text, and later had uneven spacing around the action
  icon that I put in place. The cause was some of the settings that I forgot to
  adjust in the parent border.
- **Prompt unable to reach the HUD:** The interact system couldn't call the
  HUD because the HUD reference variable didn't exist in the player
  controller. We promoted the HUD widget to a variable and fixed a node I placed
  by mistake.
- **Pause menu not closing on a second key press:** This one is still ongoing, I'm
  not entirely sure what I messed up and will have to retrace my steps. After adding
  the interact system, this part no longer worked as intended.
- **Cursor not displaying in-game** Another ongoing issue, the cursor disappears
  after interacting with either menu. Unchecking the "Hide cursor" option brings
  that cursor back, but disables input. I likely left an incorrect node in place
  or messed up a call to focus.
  (Andrew)
- **Traps not responding to player character** Removed references to deprecated character BP
  preventing collision box interactions from triggering properly.
- **Single trap trigger activating multiple traps** Built instance-based system using public variables.
  Now each instance of each trigger (tripwire or camera) is tied to a specific targeted instance
  of the movable walls and do not interfere with each other.

(Ryan)
After creating the health system, I've been notified that the sentries Andrew had imported from his previous project were not successfully dealing damage to the player character. Being familiar with the setup I've placed, I took a look at the blueprint for the sentries' projectile myself. The logic was going in the right direction, and it took me a fair minute to figure out why it wasn't responding to the health blueprint properly. It turns out, an empty variable was created using a similar naming scheme as the blueprint and was calling to it, which explains why nothing was happening. The fix was fairly straightforward once I'd managed to crack the code, and I simply adjusted it to properly call out to the health blueprint instead of the variable. 

### In terms of the QA and testing process, what would you do differently?

(Zach)
We would test earlier and more often rather than building several systems before
testing, since one change affected another in this case. Unfortunately, this is very
difficult to do since our schedules are entirely different across the team.


### What tools (chosen in Module Two) did you find successful, and why?

(Zach)
- **Blueprints:** Allowed fast iteration on gameplay and UI
  without waiting on compile times, and Blueprint Interfaces made it easy to
  add new interactable object types.
- **CommonUI plugin:** Provided a consistent structure for menus and input
  handling.
- **GitHub:** My first experience with a team project using github and it's fantastic.
  Easy to access and update the project for us all using git.

(Andrew)
- **Discord** Discord has facilitated quick and easy communication for when merge requests have been made
  or for general progress updates between team members.

(Ryan)
- **Tasklist:** Creating a task list through a seperate, viewable Google Doc was very handy when laying out current tasks for team members to achieve throughout the week. 

### Were there any tools or techniques that were not helpful, and why?

(Zach)
CommonUI added setup overhead (viewport client, input data, stacks)
and caused some early bugs that I had to deal with because I hadn't decided to use
the plugin from the start, so merging/switching over took a bit of tinkering.

(Andrew)
Some assets were migrated from a prior project. The previous project was of a very different design
and nature so had several dependencies that made them difficult or impossible to adapt. While a few did adapt easily and nicely,
some time was wasted on a one or two items I decided to ultimately scrap altogether,
such as a physics-based pick up the player could carry and drop.
### How did the initial analysis of the game design document contribute to the decision to use these tools and techniques?

(Zach)
Our game design document had requirements for menus, a HUD, interactables, etc. that just
made CommonUI seem like a no-brainer to me. The plugin made it (somewhat) easy to set up
a modular widget structure.

