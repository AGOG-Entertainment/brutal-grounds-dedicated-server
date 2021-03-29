# Brutal Grounds Dedicated Server

## Platforms
Brutal Grounds Dedicated Server is supported for both Linux and Windows.

## Quickstart- Where to get it
In order to download the Brutal Grounds Dedicated Server, you need to have access to Brutal Grounds on Steam.

### Steam Library
1. In Steam, set your Library filters to enable Tools
2. Download Brutal Grounds Dedicated Server
3. Right click Brutal Grounds Dedicated Server -> Properties
4. Under Launch Options put `-log -nullrhi`
5. Launch Brutal Grounds Dedicated Server from the Steam Library

### Steamcmd (Advanced)
[Steamcmd is a command line interface](https://developer.valvesoftware.com/wiki/SteamCMD), primarily used for managing dedicated servers on Steam.
1. Follow Valve's official instructions on how to install Steamcmd
2. `steamcmd +login +force_install_dir ../brutal_grounds_ds +app_update 1123110 +quit`

## Ports
### Default Ports
- `7777`(UDP) Game Traffic
- `27015`(UDP) Server Browser Query

### Launch Params
- `-Port=` Sets the Game Traffic port
- `-QueryPort=` Sets the Server Browser Query port
  - You can alternatively set `-QueryPort=` to `-1` to share packets with the Game Traffic port. This means you would only need to forward one port.
- `-ExternalGamePort=` Sets the _external_ game port, particularily for when behind a NAT.

### Behind a NAT
When you're behind a NAT you might neet to use `-ExternalGamePort=`. And you need to use `-QueryPort=-1`. This tells the Steam Master Server what your external port is so that clients know how to connect from the Server Browser.

## Configuration
As of right now the configuration is very limited, but here's a list of available launch paramaters.
- `-log` (Recommended) Outputs the server to the log.
- `-nullrhi` (Recommended) Tells the server to not try and allocate memory on the GPU.
- `-AdminId=` (Recommended) Sets the Admin ID(s) for the server which allows you to control the server when connected to it in-game. This method is very temporary and we plan on making it more robust in the future.
  - The ID it expects is a Steam 64 bit ID. You can use [Steam ID Finder](https://steamidfinder.com) to find your SteamID. Copy the `steamID64 (Dec)` value.
  - Expects a string, and can accept an array of IDs comma separated.
- `-SteamServerName=` Sets the server name in the server browser. Expects a string.
- `-HostName=` Sets the name of the host in the server browser. Expects a string.
- `-Port=` Sets the game traffic port.
- `-QueryPort=` Sets the query port.
- `-ExternalGamePort=` Sets the external game port. If setting this, you should also use `-QueryPort=-1`.
- You also have all existing [Unreal Engine 4 launch paramaters](https://docs.unrealengine.com/en-US/ProductionPipelines/CommandLineArguments/index.html) available to Shipping builds.

### Setting starting map and game mode
The first paramater when launching the server is the map name. You can also specify the game mode.
**NOTE:** Some maps support multiple game modes, but you can run into problems if you specify a game mode it doesn't support!

Linux example: `./BrutalGroundsServer.sh Arena -log -nullrhi`
Windows example: `./BrutalGroundsServer.exe Arena -log -nullrhi`

### Map Names
**NOTE:** The naming convention is not standardized and is subject to change for consistency.
- Arena
- ArenaCTF
- ArenaRelic
- Avaris
- Frost
- FrostDM
- Meltdown
- NorthPoint
- Pit
- Ruins
- RuinsCompacted
- ShiftingSandsControl
- ShiftingSandsCTF
- ShiftingSandsDM
- SkyTemple
- Tomb
- Tower
- Plateau1
- TheCourt
- Canyon

## Controlling Server
### Command Centre - Controlling from In-Game
You must set the `-AdminIds=` launch paramater. Launch the game from a Steam account matching an ID specified in `-AdminIds`. Connect to the server and press `esc` to access the escape menu, go to `Command Centre`.

### RCON
There is no RCON available yet but it's a planned feature.

## Planned Features
In no particular order, here are some planned features:
- RCON Client
- Kick, Ban players
- Chat logs
- Welcome message
- Config files
