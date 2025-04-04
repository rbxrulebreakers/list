> [!CAUTION]
> The only official place to get the rbxrulebreakers list is https://github.com/rbxrulebreakers/list. Any other websites offering downloads or claiming to be us are not controlled by us.

> [!WARNING]
> We are not Roblox employees! If you require assistance from Roblox then [click here](https://www.roblox.com/support) or call roblox (United States Number) at 888-858-2569.

> [!IMPORTANT]
> This repository is created for informational, educational, moderation, and safety purposes only. This repository is not intended to target, harass or bully any individual mentioned. We strongly condemn harassment, bullying, raiding and any form of online misconduct. Users are reminded to engage respectfully and responsibly.

![Adudu21's Roblox Rule Breakers](https://github.com/user-attachments/assets/076a06b6-0c77-448b-bea2-286d24ea2dc5)

[![Discord Server][shield-discord-server]][discord-invite]

# Roblox Exploiters and Terms of Use/Community Standards Violators List 
A list of users which violate the rules of Roblox (that could be considered serious violations) so you can prevent them from joining your Roblox Game(s)

# ❗Reports and Appeals📄
> [!TIP]
> **Before requesting for a user to be added into the list, it's recommended to also use Roblox's Reporting Features, if you're within the EU, you may visit https://www.roblox.com/illegal-content-reporting then afterwards report the user there (EU Reports have a higher chance to be accepted than regular roblox reports).**

You can report and appeal within the [![Discord Server][shield-discord-server]][discord-invite].

> [!CAUTION]
> **Reports, Appeals or such are carefully and fairly reviewed. Tickets that do not follow the guidelines may result getting ticket blacklisted or such.**

> [!NOTE]
> **Terminated users might be removed from the list, if a user was removed because of being terminated but is now unterminated, you can request for them to be readded into the list.**

# ❓Quick FAQ
Q: "You're adding everyone into the list!"

A: We do not "add everyone" into the list, we only add users which have Exploited in Roblox Experiences ("Games"), ERP'ed or such. Users are flagged for review if they are friends with any accounts that are within the list. If you really do not trust such a list, you are not forced to use it.

Q: What is this for?

A: To prevent individuals that can harm your playerbase or such.

Q: Why and when did this exist?

A: The RbxRuleBreakers List has been active since [November 17, 2024](https://github.com/adudu21isme/rbxrulebreakers/commit/958cf0ccd9ac6bdf826dff0d09dc4097a7ccbaa1). The reason why this was created is because [adudu21](https://www.roblox.com/users/684075566/profile) had gotten tired of how many rule breakers exist that were not moderated by Roblox and as-well was inspired by MFD (another project/organization, created by Ruben).

> [!TIP]
> You may find more frequently asked questions within the [![Discord Server][shield-discord-server]][discord-invite].

# General information
This is a list with Roblox UserId(s), Roblox UserId(s) are PUBLIC INFORMATION.

This list is made for Roblox Game Developers to use it.

Official Roblox Community/Group for rbxrulebreakers is https://www.roblox.com/communities/35633326/rbxrulebreakers

# Usage
> [!NOTE]
Join the [![Discord][shield-discord-server]][discord-invite] Server before using the list for your game(s).

> [!IMPORTANT]
> These are examples. The game must have HTTP Requests Enabled otherwise it will not work.

> [!Tip]
> If your game has at-least 500K Visits and 1K+ DAU ("Daily Active Users"), you can create an inquiry within the [![Discord][shield-discord-server]][discord-invite] Server for it to be listed in https://devforum.roblox.com/t/adudu21s-rbxrulebreakers-list/3506160. 
## Fetch list
> [!NOTE]
> Outputs the list.
```luau
print(game:GetService("HttpService"):GetAsync("https://raw.githubusercontent.com/rbxrulebreakers/list/main/users"))
```
## Using the list
> [!NOTE]
> Prevents users which are within the list from joining your Roblox Game
```luau
--// Services
local http = game:GetService("HttpService")
local plrs = game:GetService("Players")

--// Vars
local fetching,list = nil,nil

--// Functions

-- Fetches the latest list of https://github.com/rbxrulebreakers/list
@native
local function FetchList()
   if fetching then while task.wait(1) do if not fetching then return end end end
   fetching=true
   local s,r,t=nil,nil,3
   repeat
      s,r=pcall(function()
         return http:GetAsync("https://raw.githubusercontent.com/rbxrulebreakers/list/main/users",true)
      end)
      if not s then
         if string.match(r,"exceeded") then warn("RATELIMIT. Waiting 30 seconds...")task.wait(30)else t=-1 task.wait(1)end
      end
   until s or t == 0
   if s then list=r end
   fetching=nil
end

-- Checks if the user is on the list.
@native
local function IsOnList(id)
   return list and string.match(list,`,{id},`)
end

--// When new players join
plrs.PlayerAdded:Connect(function(p)
   local id = p.UserId
   --// Is User on list? Put this somewhere that its ok if the code yields
   if not list then FetchList()end
   if IsOnList(id) then
      --// Kick the rule breaker from the game
      return p:Kick([[Violations of Roblox's ToU ("Terms of Use")/Community Standards or similar.

Moderating any users associated with RbxRuleBreakers (RRB) will not remove you from the list.

To appeal, join the RbxRuleBreakers Discord Server, to find it, visit GitHub and search rbxrulebreakers/list then read README.md. If appeal is accepted, you'll be allowed to play again in approximately 2 hours.]])
   end
end)

--// Update list cache every hour
task.spawn(function()
   while task.wait(3600) do
      FetchList()
   end
end)
```
[shield-discord-server]: https://img.shields.io/discord/1335018287209123890?logo=discord&logoColor=white&label=discord&color=000000
[discord-invite]: https://discord.gg/U7JstgHdyg