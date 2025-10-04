-- TradingTicketSpawner.lua
-- Template: palitan ang Remote name at parameters ayon sa actual game.

local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local plr = Players.LocalPlayer

-- === CONFIG ===
local PET_IDS_TO_SPAWN = {101, 102, 103} -- example pet IDs; palitan ayon sa gusto mo
local AMOUNT_PER_PET = 1
local DELAY_BETWEEN = 0.3

-- === MODIFY THIS to match the game's remote you want to call ===
-- Example: if the game has ReplicatedStorage.Remotes.SpawnPet:FireServer(petId, amount, ticketType)
local function spawnPet(petId, amount)
    -- safe placeholder: change this line to the actual remote call used by the game
    local remote = ReplicatedStorage:FindFirstChild("Remotes") and ReplicatedStorage.Remotes:FindFirstChild("SpawnPet")
    if remote and typeof(remote.FireServer) == "function" then
        -- Example call; adjust parameters to what the game's remote expects
        remote:FireServer(petId, amount, "TradingTicket")
    else
        warn("Spawn remote not found. Edit this script to point to the game's spawn remote.")
    end
end

-- Main loop
for _, id in ipairs(PET_IDS_TO_SPAWN) do
    spawnPet(id, AMOUNT_PER_PET)
    wait(DELAY_BETWEEN)
end
