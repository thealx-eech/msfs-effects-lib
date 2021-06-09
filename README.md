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

3. Copy "VisualEffectLibs" folder into your aircraft folder, remove effects you don't need, regenerate JSON files
4. You can load project in MSFS Effects Editor to apply labels replacement and effect parameters adjustment, then build package and repeate step #3
5. To avoid conflicts, it is recommended to update effect GUIDs and rebuild package


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
		<Component ID="FX_SMOKE_LEFT">
			<Component ID="FX_SMOKE_LEFT_NODE" Node="LIGHT_ASOBO_Navigation_Red">
				<UseTemplate Name="ASOBO_GT_FX">
					<FX_CODE>1</FX_CODE>
					<FX_GUID>{600252C7-538F-45A7-9B57-58C7D6DF4B7C}</FX_GUID>
				</UseTemplate>
			</Component>
		</Component>
		<Component ID="FX_SMOKE_RIGHT">
			<Component ID="FX_SMOKE_RIGHT_NODE" Node="LIGHT_ASOBO_Navigation_Green">
				<UseTemplate Name="ASOBO_GT_FX">
					<FX_CODE>1</FX_CODE>
					<FX_GUID>{9CA5EFF5-30EE-4978-83FF-3517689E0C33}</FX_GUID>
				</UseTemplate>
			</Component>
		</Component>		
```
Where FX_GUID #1 taken from "Aerobatics Smoke White.xml", FX_GUID #2 - from "Aerobatics Smoke Blue.xml"

Node ID found in glTF file

All ID should be unique

You can attach same affect to different nodes, or different effects to same node

6. Copy content of "Packages" into your Community folder

7. Start the game, to activate effect - use mentioned SimVar trigger by gauge script, simconnect, or existing hotkey


# Table of content:

1. AerobaticsSmoke

  1.1 Type: ribbon + particles

  1.2 Included effects: 4
  
  red: {C4A0D249-1F33-4581-99C4-2DF4FC625C6F}
  
  green: {AE15BEB6-BD51-4B22-9542-287E27DC26BA}
  
  blue: {9CA5EFF5-30EE-4978-83FF-3517689E0C33}
  
  white: {600252C7-538F-45A7-9B57-58C7D6DF4B7C}

  1.3 Rate: varialbe (2 particles per each 10 meters)

  1.4 SimVar trigger: LIGHT WING

  1.5 Capacity: 4000 (reached at airspeed ~ 500kn)

  1.6 Rendering distance: 5000m

  1.7 Lifetime: 30s

  1.8 Affected by wind: yes

  1.9 Work in multiplayer: unconfirmed
  
  1.10 Meterial: ContrailSmoke, ContrailSmokeNear
  
  1.11 Demo: https://youtu.be/sMKvOmudbyI
