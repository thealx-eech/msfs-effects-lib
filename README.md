# msfs-effects-lib

Effects library for Microsoft Flight Simulator

License: MIT, free to use in any freeware or payware projects. No credits required.

# 4.08.2021
# PROJECT FROZEN
# until ASOBO fix stability issues of FX editor

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

6. Copy content of "Packages" into your Community folder (for example "touchingcloud-effect-exhaust-smoke")

7. Start the game, to activate effect - use mentioned SimVar trigger by gauge script, simconnect, or existing hotkey


# Table of content:

# 1. AerobaticsSmoke (SU5 compatible)

  1.1 Type: ribbon + sprites

  1.2 Included effects: 4
  
  red: {C4A0D249-1F33-4581-99C4-2DF4FC625C6F}
  
  green: {AE15BEB6-BD51-4B22-9542-287E27DC26BA}
  
  blue: {9CA5EFF5-30EE-4978-83FF-3517689E0C33}
  
  white: {600252C7-538F-45A7-9B57-58C7D6DF4B7C}

  black: {F5B8D8FA-C9AB-4D3A-A9F7-F1C2AB452CA3}
  
  orange: {20C1D0CF-40F8-4ED9-A2C7-E008FFE1F6AF}

  1.3 Rate: varialbe (2 particles per each 10 meters)

  1.4 SimVar trigger: none

  1.5 Capacity: 2000 (reached at airspeed ~ 500kn)

  1.6 Rendering distance: 5000m

  1.7 Lifetime: 30s

  1.8 Affected by wind: yes

  1.9 Work in multiplayer: yes
  
  1.10 Meterial: ContrailSmoke, ContrailSmokeNear
  
  1.11 Demo: https://youtu.be/sMKvOmudbyI
  
# 2. TyreSpray (SU5 incompatible)

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

# 3. EngineExhaust (SU5 incompatible)

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

# 4. Downwash (SU5 incompatible)

  4.1 Type: sprites
  
  4.2 Included effects: 1
  
  {936C9B32-A095-47F6-9619-15D8EE073614}
  
  4.3 Rate: 2/s
  
  4.4 SimVar trigger: turb/piston engine RPM > 0 && altitude < 50
  
  4.5 Capacity: 100
  
  4.6 Rendering distance: 2000m
  
  4.7 Lifetime 2s
  
  4.8 Affected by wind: no
  
  4.9 Work in multiplayer: unconfirmed
 
  4.10 Material: ContrailSmokeNear
  
  4.11 Demo: https://youtu.be/3Zlf6Wc92qc
 