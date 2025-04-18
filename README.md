====================
GrowServer Documentation
====================

Author: Gnome
Version: 1.0
Last Updated: April 2025

--------------------
📦 Server Overview
--------------------
GrowServer is a custom multiplayer server that mimics core functionalities of Growtopia. It uses a custom TCP/UDP network structure and supports a range of in-game commands and packet responses.

--------------------
🧩 Packet Types
--------------------

1. **dialogrequest**
   - Used to send a dialog box to the client.
   - Format:
     ```
     add_callback("OnDialogRequest");
     add_string("add_label_with_icon|big|Welcome to GrowServer!|left|123\nadd_textbox|Hello, enjoy your stay!\nadd_button|Okay|btn_ok|Cancel|btn_cancel\nend_dialog|server_dialog|btn_ok|btn_cancel");
     send_packet(2);
     ```

2. **onConsoleMessage**
   - Sends a message to the client console.
   - Format: `add_string("` + message + `"); send_packet(3);`

3. **action**
   - Handles in-game actions like placing blocks, using items, etc.

--------------------
📜 Command List
--------------------

- `/give <itemID> <amount>`
  - Gives item to the player.

- `/find <itemName>`
  - Searches for an item by name and shows the ID.

- `/ban <GrowID>`
  - Bans the specified player.

- `/unban <GrowID>`
  - Unbans a previously banned player.

--------------------
🛠️ How to Add a New Command
--------------------
1. Go to the command handler file (usually `CommandProcessor.cpp`).
2. Add a new condition for your command:
   ```cpp
   else if (command == "/example") {
       player->SendConsoleMessage("This is a test command.");
   }
   ```
3. Recompile the server.

--------------------
💬 Dialog Request Structure
--------------------
Use the following structure to send dialog windows to the client:

```
add_callback("OnDialogRequest");
add_string("add_label_with_icon|big|Title Text|left|602\nadd_textbox|This is an example dialog.\nadd_text_input|label|default text|textinput_id\nadd_button|OK|btn_ok|Cancel|btn_cancel\nend_dialog|dialog_id|btn_ok|btn_cancel");
send_packet(2);
```

--------------------
🔐 Security Notes
--------------------
- DDoS protection is built-in and monitors UDP/TCP for abuse.
- Clients spamming requests are automatically blacklisted.
- All failed protections are logged in `fail.txt`.

--------------------
📁 File Structure
--------------------
- `players/`
  - Stores GrowID files containing player data.
- `logs/`
  - Contains logs from the server activity.
- `config/`
  - Configuration files for ports and server settings.

--------------------
🔌 Ports Used
--------------------
- **TCP:** 17091 (main communication)
- **UDP:** 17092 (for pings and position updates)

--------------------
📈 Tips for Expanding the Server
--------------------
- Add more in-game events with custom `dialogrequest`s.
- Integrate with a web panel for admin tools.
- Extend item database for custom items.
- Track player IPs and detect proxies/VPNs.

====================
End of Documentation
====================

