local HttpService = game:GetService('HttpService')
local Players = game:GetService('Players')
local LocalPlayer = Players.LocalPlayer

local username = LocalPlayer.Name

game.StarterGui:SetCore("SendNotification", {
    Title = 'API Roblox Player',
    Text = 'Account ✅: ' .. username .. '\n' .. 'Robloxplayerversion',
    Icon = 'rbxassetid://13333189485'
})

local function sendData()
    print([[

 _______   _______         _______   ___            __       ___  ___  _______   _______   
/"      \ |   _  "\       |   __ "\ |"  |          /""\     |"  \/"  |/"     "| /"      \  
|:        |(. |_)  :)      (. |__) :)||  |         /    \     \   \  /(: ______)|:        | 
|_____/   )|:     \/       |:  ____/ |:  |        /' /\  \     \\  \/  \/    |  |_____/   ) 
 //      / (|  _  \\       (|  /      \  |___    //  __'  \    /   /   // ___)_  //      /  
|:  __   \ |: |_)  :)     /|__/ \    ( \_|:  \  /   /  \\  \  /   /   (:      "||:  __   \  
|__|  \___)(_______/     (_______)    \_______)(___/    \___)|___/     \_______)|__|  \___) 

    ]])

    local data = {
        Username = username
    }

    local jsonData = HttpService:JSONEncode(data)
    local url = "http://127.0.0.1:2568/Xrlogdes_Data"

    local success, response = pcall(function()
        return (syn and syn.request or request or (http and http.request) or http_request)({
            Url = url,
            Method = "POST",
            Headers = {
                ["Content-Type"] = "application/json"
            },
            Body = jsonData
        })
    end)

    if success and response.StatusCode == 200 then
        print("Successful")
        game.StarterGui:SetCore("SendNotification", {
            Title = 'Success ✅',
            Text = 'Connect To Program Successful',
            Icon = 'rbxassetid://13333189485'
        })
    else
        print("Failed")
        game.StarterGui:SetCore("SendNotification", {
            Title = 'ERROR ❌',
            Text = 'Connect To Program Failed',
            Icon = 'rbxassetid://13333189485'
        })
    end
end

while wait(10) do
    sendData()
end
