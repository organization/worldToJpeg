# worldToJpeg
 마인크래프트맵을 간단한 소스를 통해 이미지처리합니다
```
BufferedImage image;
				try {
					image = new BufferedImage(600, 600, BufferedImage.TYPE_INT_RGB);
					Graphics2D graphics = image.createGraphics();
					Position spawn = getServer().getDefaultLevel().getSafeSpawn();
					/**
					*스폰위치 반경으로 x,z좌표를 ±300 만큼 graphics인스턴스에 넣어줍니다
					*/
					for (int x = 0; x < 600; x++) {
						for (int y = 0; y < 600; y++) {
							graphics.setColor(getServer().getDefaultLevel().getMapColorAt(spawn.getFloorX() - 300 + x,
									spawn.getFloorZ() - 300 + y));
							graphics.fillRect(x, y, x, y);
						}
					}
					/**
					 * 플레이어를 인식하면 해당 플레이어의 위치와 그 닉네임을 추가로 이미지에 반영합니다
					 * 해당 기능을 원치않을경우 작성하지 않으시면 됩니다
					 */
					for (Player player : getServer().getOnlinePlayers().values()) {
						int x = player.getPosition().getFloorX();
						int y = player.getPosition().getFloorZ();
						Position spawn1 = getServer().getDefaultLevel().getSafeSpawn();

						if (x <= spawn1.getFloorX() + 300 && x >= spawn1.getFloorX() - 300
								|| y <= spawn1.getFloorZ() + 300 && y >= spawn1.getFloorZ() - 300) {

							graphics.setColor(Color.RED);
							graphics.fillRect((spawn.getFloorX() - x) + 299, (spawn.getFloorZ() - y) + 299, 2, 2);
							graphics.setColor(Color.BLACK);
							graphics.drawString(player.getName(), (spawn.getFloorX() - x) + 300,
									(spawn.getFloorZ() - y) + 296);

						}
					}
					try {
						File file = new File(getDataFolder() + "/world.jpeg");
						ImageIO.write(image, "jpeg", file);
						getLogger().info("finsh");
					} catch (IOException e) {
					return;
					}
				} finally {
				}
```
![logo](https://github.com/organization/worldToJpeg/blob/master/PicsArt_10-02-04.05.52.png)
