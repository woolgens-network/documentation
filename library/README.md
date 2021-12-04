# [ Woolgens-library ](https://github.com/woolgens-network/library) docs

## Table of contents
- [ Commands ](#commands)
- [ GUIs ](#gui)
- [ NPCs ](#npc)

<a name="commands"></a>
## Commands

```java
public class TestCommand extends SpigotCommand<Player> {

    public TestCommand() {
        super("yeet");
    }

    @Override
    public boolean send(Player player, SpigotArguments arguments) throws CommandException {
        player.sendMessage("Yeet");
        return true;
}
```

### Help command builder

```java
public class TestCommand extends HelpCommand<Player> {

    public TestCommand() {
        super("test", "Test");
        setSenders(Player.class);
        addChild(new AddSubCommand());
    }
}
```

#### Add a subcommand

```java
public class AddSubCommand extends HelpSubCommand<Player> {


    public AddSubCommand() {
        super("add");
        setUsage("<name>");
        setDescription("Add a player");
    }

    @Override
    public boolean send(Player player, SpigotArguments spigotArguments) throws CommandException {
        player.sendMessage("I'm Gay");
        return true;
    }
}
```

<a name="gui"></a>
## GUIs

```java
GUI gui = new GUI("§aYeet", 3);
gui.addStatelessButton(13, new ItemBuilder(Material.APPLE).setName("§aStateless Button").build(), new ClickButtonEvent() {
    @Override
    public void onClick(Player player, InventoryClickEvent event) {
        player.sendMessage("Yeet");
    }
});

gui.build();
gui.openInventory(player, Sound.BLOCK_CHEST_OPEN);
```

### Stateful

```java
GUI gui = new GUI("§aYeet", 3);

String balance = gui.useState("balanace", 0);

gui.addStatefulButton(13, () -> new ItemBuilder(Material.IRON_AXE)
        .setName("Balanace: " + gui.getState(balance)).build(), new ClickButtonEvent() {
    @Override
    public void onClick(Player player, InventoryClickEvent inventoryClickEvent) {
        int balanceMoney = gui.getState(balance);
        gui.setState(balance, balanceMoney + 1);
    }
}, balance);

gui.addStatefulButton(4, () -> new ItemBuilder(Material.APPLE)
        .setName("Yeets: " + gui.getState(balance)).build(), balance);

gui.build();
gui.openInventory(player, Sound.BLOCK_CHEST_OPEN);
```

<a name="npc"></a>
## NPCs

### Skin by username

```java
NPC npc = new NPC(player.getLocation(), "Maga");
npc.setGameMode(NPC.Gamemode.SURVIVAL);
NPC.SkinTextures.getByUsername("ReaperMaga").thenAccept(skinTextures -> {
   npc.setSkin(skinTextures);
    NPCWrapper wrapper = new NPCWrapper(npc);
    wrapper.setLooking(true);
    wrapper.setListener(player1 -> player1.sendMessage("Working!"));
    wrapper.build();
}).exceptionally(e -> null);
```

### Skin by signature and value

```java
NPC npc = new NPC(player.getLocation(), "Maga");
npc.setGameMode(NPC.Gamemode.SURVIVAL);
npc.setSkin(new NPC.SkinTextures("value", "signature"));
NPCWrapper wrapper = new NPCWrapper(npc);
wrapper.setLooking(true);
wrapper.setListener(player1 -> player1.sendMessage("Working!"));
wrapper.build();
```
