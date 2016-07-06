Bulunuz:" function aAction " ve değiştirin:

function aAction ( type, action, admin, player, data, more )
    if ( aLogMessages[type] ) then
        function aStripString ( string )
            string = tostring ( string )
            string = string.gsub ( string, "$admin", getPlayerName ( admin ):gsub("#%x%x%x%x%x%x","") )
            string = string.gsub ( string, "$by_admin_4all", isAnonAdmin4All( admin )    and "" or " by " .. getPlayerName ( admin ):gsub("#%x%x%x%x%x%x","") )
            string = string.gsub ( string, "$by_admin_4plr", isAnonAdmin4Victim( admin ) and "" or " by " .. getPlayerName ( admin ):gsub("#%x%x%x%x%x%x","") )
            string = string.gsub ( string, "$data2", more or "" )
            if ( player ) then string = string.gsub ( string, "$player", getPlayerName ( player ) ) string = string:gsub("#%x%x%x%x%x%x","") end
            return tostring ( string.gsub ( string, "$data", data or "" ) )
        end
        local node = aLogMessages[type][action]
        if ( node ) then
            local r, g, b = node["r"], node["g"], node["b"]
            if ( node["all"] ) then outputChatBox ( aStripString ( node["all"] ), _root, r, g, b ) end
            if ( node["admin"] ) and ( admin ~= player ) then outputChatBox ( aStripString ( node["admin"] ), admin, r, g, b ) end
            if ( node["player"] ) then outputChatBox ( aStripString ( node["player"] ), player, r, g, b ) end
            if ( node["log"] ) then outputServerLog ( aStripString ( node["log"] ) ) end
        end
    end
end
