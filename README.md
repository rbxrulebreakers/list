RbxRuleBreakers is not partnered with Roblox and is not endorsed by Roblox. If you require assistance from Roblox then [click me](https://www.roblox.com/support).

# Information within this repository is subject to change.

![Adudu21's Roblox Rule Breakers](https://github.com/user-attachments/assets/076a06b6-0c77-448b-bea2-286d24ea2dc5)

[![Discord Server][shield-discord-server]][discord-invite]

# Roblox Exploiters and Terms of Service/Community Standards Violators List 
> A list of users which violates the rules of roblox (that can be considered serious violations) so you can prevent them from joining your Roblox Game

# ❗Reports and Appeals📄
**Before requesting for a user to be added onto the list, it's suggested that you use Roblox's Reporting Features, if you're in the EU, you can visit https://www.roblox.com/illegal-content-reporting and afterwards report the user to roblox there (EU Reports have a higher chance to be accepted than regular roblox reports).**

You can report and appeal in [![Discord Server][shield-discord-server]][discord-invite].

**Users are ONLY added if they actually broke the rules. Reports and appeals are carefully read if it's a legitimate report/appeal.**

**Terminated users are likely to be removed from the list. If a user was terminated but has been unterminated and was in the list, you can request for them to be readded.**

# ❓Quick FAQ
Q: "You're adding everyone into the list!"

A: We do not "add everyone" into the list, we only add users which have exploited in roblox games, ERP'ed or did very bad actions. We have responsible individuals reviewing reports and such. Users are flagged for review if they are friends with any bad account on the list. If you really do not trust such a list, you are not forced to use it.

Q: What is this for?

A: To prevent individuals that can harm your playerbase or such.

Q: Why and when did this exist?

A: The RbxRuleBreakers List has been active since [November 17, 2024](https://github.com/adudu21isme/rbxrulebreakers/commit/958cf0ccd9ac6bdf826dff0d09dc4097a7ccbaa1). The reason why this was created is because adudu21 had gotten tired of how many rule breakers exist and was as-well inspired by Moderation For Dummies (another project/organization, created by Ruben Sim).

You may find more questions within [![Discord Server][shield-discord-server]][discord-invite].

# General information
This is a list with Roblox UserId(s), Roblox UserId(s) are PUBLIC INFORMATION.

This list is made for Roblox Game Developers to use it.

Official Roblox Community/Group for rbxrulebreakers is https://www.roblox.com/communities/35633326/rbxrulebreakers

##  This is to let you know what would count as a violation (not all is listed)

1. Violations that would result in permanent suspension from Roblox
2. Exploiting (using third-party software to tamper with Roblox. If a user is detected for cheating in a roblox game affiliated with adudu21, they may be added into the list)
3. Excessive Harmful Toxicity (Bullying, Harassment, Threats)
4. Excessive Harmful Misinformation
5. Mass Scamming

Every once in awhile or so, the status's of the users in the list will be checked (including Bio ("About me") for harmful content), additionally, their friends Bios ("About me") may aswell be checked for harmful content. To the providers of the services that are used to check, a header named "X-FriendChecker" alongside "X-Checker" is provided.

# Usage
Please join the [![Discord][shield-discord-server]][discord-invite] Server before using the list for your game(s), if there's any important announcements or such, you'll be notified there.
> These are examples. The game must have HTTP Requests Enabled.

> If your game has at-least 500K Visits and 1000+ DAU ("Daily Active Users"), you may create an inquiry within the Discord Server for it to be listed in https://devforum.roblox.com/t/adudu21s-rbxrulebreakers-list/3506160. 
## Fetch list
> Outputs the list.
```luau
print(game:GetService("HttpService"):GetAsync("https://raw.githubusercontent.com/rbxrulebreakers/list/main/users"))
```
## Prevent players in the list from joining

```luau
--// Services
local http = game:GetService("HttpService")
local plrs = game:GetService("Players")

--// Vars
local fetching = nil
local list = nil

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
         if string.match(r,"exceeded") then warn("⚠️RBX RATELIMIT. Waiting 30sec...")task.wait(30)else t=-1 task.wait(1)end
      end
   until s or t == 0
   if s then list=r end
   fetching=nil
end

-- Checks if the user is on the list. Use Parallel Luau?
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
      return p:Kick([[Violations of Roblox ToS ("Terms of Service")/Community Standards or similar.

Banning the owner and/or such from your game(s) will not remove you from the list and will not improve your ego.

You can appeal via joining the Discord Server, to find it, go to rbxrulebreakers/list on GitHub then afterwards check README.md, if appeal is accepted, you'll be allowed to play again in approximately 1 hour.]])
   end
end)

--// Update list cache every hour
task.spawn(function()
   while task.wait(3600) do
      FetchList()
   end
end)
```

# This repository is created for informational, educational, moderation, and safety purposes only. This repository is not intended to target, harass or bully any individual mentioned. We strongly condemn harassment, bullying, raiding and any form of online misconduct. Users are reminded to engage respectfully and responsibly.

[shield-discord-server]: https://img.shields.io/discord/1335018287209123890?logo=discord&logoColor=white&label=discord&color=000000
[discord-invite]:  https://discord.gg/U7JstgHdyg
