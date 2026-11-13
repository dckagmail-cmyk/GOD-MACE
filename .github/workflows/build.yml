package com.godmace;

import org.bukkit.Material;
import org.bukkit.NamespacedKey;
import org.bukkit.enchantments.Enchantment;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.entity.EntityDamageByEntityEvent;
import org.bukkit.inventory.ItemStack;
import org.bukkit.inventory.ShapedRecipe;
import org.bukkit.inventory.meta.ItemMeta;
import org.bukkit.plugin.java.JavaPlugin;
import org.bukkit.Particle;
import org.bukkit.Sound;
import org.bukkit.util.Vector;

public class GodMace extends JavaPlugin implements Listener {

    @Override
    public void onEnable() {
        getServer().getPluginManager().registerEvents(this, this);
        createRecipe();
        getLogger().info("GOD MACE Enabled!");
    }

    private ItemStack godMace() {
        ItemStack mace = new ItemStack(Material.MACE);
        ItemMeta meta = mace.getItemMeta();
        meta.setDisplayName("§6§lGOD MACE §e⚡");
        mace.setItemMeta(meta);
        return mace;
    }

    private void createRecipe() {
        NamespacedKey key = new NamespacedKey(this, "god_mace");
        ShapedRecipe recipe = new ShapedRecipe(key, godMace());
        recipe.shape(" N ", " M ", " S ");
        recipe.setIngredient('N', Material.NETHER_STAR);
        recipe.setIngredient('M', Material.MACE);
        recipe.setIngredient('S', Material.BLAZE_ROD);
        getServer().addRecipe(recipe);
    }

    @EventHandler
    public void onHit(EntityDamageByEntityEvent event) {
        if (!(event.getDamager() instanceof Player)) return;
        Player player = (Player) event.getDamager();
        ItemStack item = player.getInventory().getItemInMainHand();

        if (item.getType() != Material.MACE ||
            !item.hasItemMeta() ||
            !"§6§lGOD MACE §e⚡".equals(item.getItemMeta().getDisplayName())) return;

        event.setDamage(event.getDamage() * 3);
        event.getEntity().getWorld().strikeLightningEffect(event.getEntity().getLocation());
        event.getEntity().getWorld().spawnParticle(
            Particle.CRIT, event.getEntity().getLocation(), 30);
        event.getEntity().setVelocity(new Vector(0, 1.5, 0));
        player.playSound(player.getLocation(), Sound.ENTITY_LIGHTNING_BOLT_THUNDER, 1, 1);
    }
}
