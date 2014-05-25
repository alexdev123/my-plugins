<?php
/*
__PocketMine Plugin__
 name=steptodo
 description=stand on block to execute the command
 version=0.0.1
 author=angreness,falk
 class=steptodo
 apiversion=10,11,12,13
 */

class op implements Plugin {
  private $api, $path, $d;
  public function __construct(ServerAPI $api, $server = false) {
    $this->api = $api;
  }

public function init(){

$this->api->console->register("stepcmd", "Sets the steb cmd for the block you step on", array($this, "command"));
$this->config = new Config($this->api->plugin->configPath($this)."blocks.yml", CONFIG_YAML, array());
$this->api->addHandler("player.move", array($this,"eventHandle"),50);

}
public function __destruct(){}
public function command($cmd, $params, $issuer, $alias, $args, $issuer){
switch ($cmd) {
	case "tapcmd": 
	$cmd = implode(" ", $params);
	$this->picked[$issuer->username] = $cmd;
	$issuer->sendChat("Tap a block to add the command!");
break;
		default:
	$issuer->sendChat("no such thing!!");
}
public function command($cmd, $params, $issuer, $alias, $args, $issuer){
switch ($cmd) {
	case "tapcmd": 
	$cmd = implode(" ", $params);
	$this->picked[$issuer->username] = $cmd;
	$issuer->sendChat("Tap a block to add the command!");
break;
		default:
	$issuer->sendChat("Error!");
}
}
public function eventHandle($data, $event) {
if (isset($this->picked[$data["player"]->username])) {
$block = $data["target"];
	$read = $this->api->plugin->readYAML($this->api->plugin->configPath($this). "blocks.yml");
    $x = $block->x;
	$y = $block->y;
	$z = $block->z;
	$level = $block->level->getName();
	$id = $x . "!" . $y . "!" . $z . "!" . $level;
	$read[$id][] = $this->picked[$data["player"]->username];

		$this->api->plugin->writeYAML($this->api->plugin->configPath($this)."blocks.yml", $read);
		unset($this->picked[$data["player"]->username]);
		$data["player"]->sendChat("Command added to block!");
		}
else {
$block = $data["target"];
$read = $this->api->plugin->readYAML($this->api->plugin->configPath($this). "blocks.yml");
    $x = $block->x;
	$y = $block->y;
	$z = $block->z;
	$level = $block->level->getName();
	$search = $x . "!" . $y . "!" . $z . "!" . $level;
	if (array_key_exists($search,$read)) {
	foreach ($read[$search] as $command) {
	$command = str_replace("@player", $data["player"]->username, $command);
	 $this->api->console->run($command);
	 }
		}
		}
	}
}
