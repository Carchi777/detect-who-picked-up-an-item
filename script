import { world, system } from "@minecraft/server"

// About this

// GitHub:          https://github.com/Carchi777/detect-who-picked-up-an-item
// Discord:         

// Made by Carchi77
// My Github:       https://github.com/Carchi777
// My Discord:      https://discordapp.com/users/985593016867778590

world.beforeEvents.entityRemove.subscribe(e => {
    const { removedEntity: entity } = e;

    const item = entity.getComponent("item")?.itemStack

    if (!item) return

    const players = entity.dimension.getEntities(
        { maxDistance: 1.5, location: entity.location, type: "player" }
    )

    players.forEach(player => {
        const inv = player.getComponent('inventory').container
        const items = Array
            .from({ length: inv.size }, (_, i) => inv.getItem(i))
            .filter(k => k != null);

        system.run(() => {
            const valid = Array
                .from({ length: inv.size }, (_, i) => inv.getItem(i))
                .filter(k => k != null)
                .some((k, i) => k.typeId === item.typeId && k.amount != items[i]);

            if (valid) {
                world.sendMessage(
                    `§i${player.nameTag} +${item.amount} ${item.typeId.slice(10)}`
                )
            }
        })
    })
})
