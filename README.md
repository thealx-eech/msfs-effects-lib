# msfs-effects-lib

Effects library for Microsoft Flight Simulator

License: MIT, free to use in any freeware or payware projects. No credits required.

# For developers - How to inject into model
1. Insert smoke nodes into aircraft exterior model (no animation required for them)
2. Add Component nodes into exterior XML inside of ```<Behaviors></Behaviors>```:


```xml
  <Include ModelBehaviorFile="Asobo\Generic\FX.xml"/>
  <Component ID="FX_SMOKE_ID">
    <Component ID="FX_SMOKE_ID_NODE" Node="model_node_name">
      <UseTemplate Name="ASOBO_GT_FX">
        <FX_CODE>1</FX_CODE>
        <FX_GUID>{EFFECT GUID}</FX_GUID>
      </UseTemplate>
    </Component>
  </Component>
```
Effect GUID can be taken from MSFS Effects editor > Templates/Instances debugger window > Asset Packages tab
or from effect XML file - InstanceId of VisualEffect.VisualEffect node (very first GUID in the file)

3.1 Copy "VisualEffectLibs" folder into your aircraft folder, remove effects you don't need, regenerate JSON files
4. You can load project in MSFS Effects Editor to apply labels replacement and effect parameters adjustment, then build package and repeate step #3
5. Rename "touchingcloud" folder, to avoid conflicts with other aircraft using same effects pack
6. It is also recommended to update effect GUIDs and rebuild package


Effects editor tutorials:

Basic ribbon smoke https://youtu.be/ohru5jw5hOo

Exhaust smoke https://youtu.be/UtqtVRw8F6Q

    
# For modders - How to attach effect to installed aircraft
1. Find exterior model glTF file, open it in text editor (like Notepad++)
2. Find the node name that probably will be suitable for your needs (like LIGHT_ASOBO_Navigation_Green), prefix like "x0_" should be removed
3. Open exterior model XML file in text editor
4. Find ```</Behaviors>``` text, if not exists - add
```xml
<Behaviors>
  
  
</Behaviors>
```
5. Before ```</Behaviors>``` insert (example for Vertigo - Turbo Prop Racer)
```xml
		<Include ModelBehaviorFile="Asobo\Generic\FX.xml"/>

		<Component ID="FX_SMOKE_RED">
			<Component ID="FX_SMOKE_RED_NODE" Node="LIGHT_ASOBO_Navigation_Red">
				<UseTemplate Name="ASOBO_GT_FX">
					<FX_CODE>1</FX_CODE>
					<FX_GUID>{C4A0D249-1F33-4581-99C4-2DF4FC625C6F}</FX_GUID>
				</UseTemplate>
			</Component>
		</Component>
		<Component ID="FX_SMOKE_NEAR_RED">
			<Component ID="FX_SMOKE_NEAR_RED_NODE" Node="LIGHT_ASOBO_Navigation_Red">
				<UseTemplate Name="ASOBO_GT_FX">
					<FX_CODE>1</FX_CODE>
					<FX_GUID>{0E5C03E0-1DC4-4AD9-B887-36200DC7FB95}</FX_GUID>
				</UseTemplate>
			</Component>
		</Component>
		
		<Component ID="FX_SMOKE_GREEN">
			<Component ID="FX_SMOKE_GREEN_NODE" Node="LIGHT_ASOBO_Navigation_Green">
				<UseTemplate Name="ASOBO_GT_FX">
					<FX_CODE>1</FX_CODE>
					<FX_GUID>{AE15BEB6-BD51-4B22-9542-287E27DC26BA}</FX_GUID>
				</UseTemplate>
			</Component>
		</Component>			
		<Component ID="FX_SMOKE_NEAR_GREEN">
			<Component ID="FX_SMOKE_NEAR_GREEN_NODE" Node="LIGHT_ASOBO_Navigation_Green">
				<UseTemplate Name="ASOBO_GT_FX">
					<FX_CODE>1</FX_CODE>
					<FX_GUID>{1E46D193-E656-4A5F-AFB3-98E214266E3A}</FX_GUID>
				</UseTemplate>
			</Component>
		</Component>
```
Where FX_GUID #1 taken from "Aerobatics Smoke White.xml",
FX_GUID #2 taken from "Aerobatics Smoke White NEAR.xml",
FX_GUID #3 - from "Aerobatics Smoke Green.xml",
FX_GUID #4 - from "Aerobatics Smoke Green NEAR.xml"

Node ID found in glTF file

All IDs should be unique

You can attach same affect to different nodes, or different effects to same node

6. Copy content of "Packages" into your Community folder (for example "touchingcloud-effect-exhaust-smoke")

7. Start the game, to activate effect - use mentioned SimVar trigger by gauge script, simconnect, or existing hotkey


# Table of content:

# 1. AerobaticsSmoke (SU6 compatible)

  1.1 Type: sprites

  1.2 Included effects: 6
  
  red trail: {C4A0D249-1F33-4581-99C4-2DF4FC625C6F}
  red near: {0E5C03E0-1DC4-4AD9-B887-36200DC7FB95}
  
  green trail: {AE15BEB6-BD51-4B22-9542-287E27DC26BA}
  green near: {1E46D193-E656-4A5F-AFB3-98E214266E3A}
  
  blue trail: {9CA5EFF5-30EE-4978-83FF-3517689E0C33}
  blue near: {2AD90D63-9E74-486D-94E4-BED83B243561}
  
  white trail: {600252C7-538F-45A7-9B57-58C7D6DF4B7C}
  white near: {8139BC0E-DAC4-47D3-9F0A-1603E6D4AD52}

  black trail: {F5B8D8FA-C9AB-4D3A-A9F7-F1C2AB452CA3}
  black near: {F5B8D8FA-C9AB-4D3A-A9F7-F1C2AB452CA3}
  
  orange trail: {20C1D0CF-40F8-4ED9-A2C7-E008FFE1F6AF}
  orange near: {31189E4A-206A-4C02-B98E-B351DC802D67}

  1.3 Rate: 1 sprites per each 5m; near - variable by velocity

  1.4 SimVar trigger: none, through XML

  1.5 Capacity: 2000 sprites

  1.6 Rendering distance: 5km sprites

  1.7 Lifetime: 30s

  1.8 Affected by wind: no

  1.9 Work in multiplayer: yes
  
  1.10 Meterial: WaterLandingFoam
  
  1.11 Demo: https://youtu.be/DczJIDfTy00?t=350
  
# 2. TyreSpray (SU6 incompatible)

  2.1 Type: sprites
  
  2.2 Included effects: 2 
  
  tyrespray: {2C46225E-CCF6-418E-8609-F532266C1872}
  
  tyresmoke: {A8381FF8-45B9-4B04-A070-FE6140074396}
  
  2.3 Rate: variable (1 per meter)
  
  2.4 SimVar trigger: none
  
  2.5 Capacity: 1000
  
  2.6 Rendering distance: 2000m
  
  2.7 Lifetime 10s/5s
  
  2.8 Affected by wind: yes
  
  2.9 Work in multiplayer: no
 
  2.10 Material: ContrailSmokeNear
  
  2.11 Demo: https://youtu.be/hOQgkqXoTsw https://youtu.be/FVipNJtf8nA

# 3. EngineExhaust (SU6 incompatible)

  3.1 Type: sprites
  
  3.2 Included effects: 4 
  
  eng1: {A3684CD6-7051-483A-B975-E580A0A180DC}
  
  eng2: {5419ABAD-8066-4A25-B5DF-030F676ADEEA}
  
  eng3: {3012A75D-0335-4AB1-9161-4E0B0883ED8E}
  
  eng4: {818AC40F-F402-40AB-86F2-8E7305C336DA}
  
  3.3 Rate: 20/s
  
  3.4 SimVar trigger: turb/piston engine RPM > 80%
  
  3.5 Capacity: 2000
  
  3.6 Rendering distance: 2000m
  
  3.7 Lifetime 30s
  
  3.8 Affected by wind: yes
  
  3.9 Work in multiplayer: unconfirmed
 
  3.10 Material: ContrailSmokeNear
  
  3.11 Demo: https://youtu.be/76QKM8j0VCg

# 4. Downwash (SU6 compatible)

  4.1 Type: sprites
  
  4.2 Included effects: 3
  
  dust {936C9B32-A095-47F6-9619-15D8EE073614}
  
  sand {7FAFB2D3-26B7-46C2-972F-D2A5A4A011B1}
  
  water & snow {D5BEC8C6-F805-4A46-ADF4-7DF97083E642}
  
  4.3 Rate: 2/s
  
  4.4 SimVar trigger: turb/piston engine #1 RPM > 0 && altitude < 50
  
  4.5 Capacity: 100 / 500 / 500
  
  4.6 Rendering distance: 2000m
  
  4.7 Lifetime 2s
  
  4.8 Affected by wind: no
  
  4.9 Work in multiplayer: unconfirmed
 
  4.10 Material: ContrailSmokeNear
  
  4.11 Demo: https://youtu.be/ZnCMCZZrl_Q
  
  4.12 Note: as downwash effect should appear near the ground instead of aircraft itself, you will reach better visuals quality if effect node will be placed between aircraft and ground level. Simplest way - create model empty node with animation where key 0 is aircraft level, key 100 - 50m below aircraft. Animation code will be "(A:RADIO HEIGHT, meters)"
 
 # 5. Waterdrop (SU6 compatible)

  5.1 Type: sprites
  
  5.2 Included effects: 3
  
  white water {35E73086-F85B-4973-8270-F686107C8422}
  
  red water {F3ADFB0B-7067-4F49-9162-72D4CD5B5073}
  
  fire source (smoke + flame) {0A9B84F3-1FC7-4B4D-9C7E-820088302E18}
  
  5.3 Rate: 100/s
  
  5.4 SimVar trigger: none
  
  5.5 Capacity: 1000
  
  5.6 Rendering distance: 2000m
  
  5.7 Lifetime 10s
  
  5.8 Affected by wind: no
  
  5.9 Work in multiplayer: unconfirmed
 
  5.10 Material: WaterLandingFoam
  
  5.11 Demo: https://youtu.be/QUkm3z1b0Ws
  
  5.12 Note: initial velocity does not work properly after SU5, you need to adjust effect heading manually; for the example video heading value was used: <FX_ROTATION_OFFSET_H>75</FX_ROTATION_OFFSET_H>
 