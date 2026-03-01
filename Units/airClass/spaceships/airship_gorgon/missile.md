[core]
@memory 坐标X: number
@memory 坐标Y: number
@memory 导弹开火时间: number
updateUnitMemory: 导弹开火时间=select(memory.导弹开火时间<1,1,memory.导弹开火时间),导弹开火时间=memory.导弹开火时间-1
updateUnitMemoryRate: 10

[turret_引导]
x: 0
y: 0
canShoot:false
canAttackFlyingUnits: false
canAttackLandUnits:   false
canAttackUnderwaterUnits: false
invisible: true
limitingRange: 2800
size: 0
[projectile_无]
areaDamage:0
areaRadius:0
targetGround:true
life: 0
deflectionPower:-1
explodeEffect:NONE
invisible:true
explodeOnEndOfLife:true

[action_导弹准备开火]
isVisible:true
price:0
text:导弹开火
description: 
displayType: action
buildSpeed: 0s
pos: 0
highPriorityQueue: false
onlyOneUnitAtATime: true
allowMultipleInQueue: false
playSoundAtUnit:start missile.wav:0.57
addActionCooldownTime:160s
fireTurretXAtGround:引导
fireTurretXAtGround_withProjectile:无
setUnitMemory:坐标X=thisActionTarget.x,坐标Y=thisActionTarget.y,导弹开火时间=50
showQuickWarLogToAllPlayers:戈尔贡导弹舱准备就绪

[hiddenAction_自动触发导弹开火]
text: 
buildSpeed: 0s
highPriorityQueue: true
autoTrigger: if self.readUnitMemory('导弹开火时间', type='number') > 27 and self.readUnitMemory('导弹开火时间', type='number') < 30
alsoQueueAction:导弹开火中1,导弹开火中2,导弹开火中3,导弹开火中4

[hiddenAction_导弹开火中1]
text: 
requireConditional: if self.readUnitMemory('导弹开火时间', type='number') > 0 and self.readUnitMemory('导弹开火时间', type='number') < 30
buildSpeed: 0.02s
highPriorityQueue: true
fireTurretXAtGround:隐藏炮塔1
fireTurretXAtGround_withProjectile:散射中介
fireTurretXAtGround_count:1
fireTurretXAtGround_withTarget:getOffsetAbsolute(x=memory.坐标X-self.x,y=memory.坐标Y-self.y)

[hiddenAction_导弹开火中2]
@copyFromSection:hiddenAction_导弹开火中1
fireTurretXAtGround:隐藏炮塔2

[hiddenAction_导弹开火中3]
@copyFromSection:hiddenAction_导弹开火中1
fireTurretXAtGround:隐藏炮塔3

[hiddenAction_导弹开火中4]
@copyFromSection:hiddenAction_导弹开火中1
fireTurretXAtGround:隐藏炮塔4

[turret_隐藏炮塔1]
x: -120
y: 135
projectile:散射中介
turnSpeed: 0
canShoot: false
canAttackFlyingUnits: false
canAttackLandUnits:   true
canAttackUnderwaterUnits: false
image:空.png
size: 0
delay: 0
canAttackMaxAngle:181
idleDir: -90
shoot_sound:ROOT:assets/sounds/rocket.ogg
shoot_sound_vol:0.46
[turret_隐藏炮塔2]
@copyFromSection:turret_隐藏炮塔1
x: 120
y: 135
idleDir: 90

[turret_隐藏炮塔3]
@copyFromSection:turret_隐藏炮塔1
x: -128
y: -118
idleDir: -90

[turret_隐藏炮塔4]
@copyFromSection:turret_隐藏炮塔1
x: 128
y: -118
idleDir: 90

[projectile_散射中介]
areaDamage:0
areaRadius:0
targetGround:true
life: 0
deflectionPower:-1
explodeEffect:NONE
invisible:true
explodeOnEndOfLife:true
spawnProjectilesOnCreate:导弹*1(offsetRandomXY=20)

[projectile_导弹]
areaDamage: 700
areaRadius: 300
image:Gorgon missile.png
life: 500
speed: 12
targetSpeed: 14
targetSpeedAcceleration: 0.2
trailEffect: CUSTOM:轨迹
trailEffectRate: 0.9
#drawUnderUnits:true
drawSize:1
turnSpeed: 6
lightSize: 0
wobbleFrequency: 4s
wobbleAmplitude: 3
targetGround: true
targetGroundSpread:400
explodeEffect: CUSTOM:命中爆炸*2,痕迹,爆炸烟雾,CUSTOM:projectileWaterSmoke*3,CUSTOM:projectileWaterSplash*3,CUSTOM:shotMark
areaRadiusFromEdge:true
areaHitAirAndLandAtSameTime:true

[effect_轨迹]
image:烟雾.png
life: 45
#fadeOut: true
fadeInTime:2
attachedToUnit: false
scaleFrom: 0.95
scaleTo: 0.9
alpha: 0.75
yOffsetRelative: -5
dirOffsetRandom: 360
xSpeedRelativeRandom: 0.05
ySpeedRelativeRandom: 0.05
xOffsetRelativeRandom: 0.5
yOffsetRelativeRandom: 0.5
total_frames: 12
animateFrameStart: 0
animateFrameEnd: 11
animateFramePingPong: false
animateFrameSpeed: 0.3
dirSpeedRandom: 0.5
priority: veryhigh

[effect_命中爆炸]
life: 50
fadeOut: true
attachedToUnit: false
alpha:0.8
scaleFrom: 1.6
scaleTo: 1.6
priority: veryhigh
image: explode.png
total_frames: 10
animateFrameStart: 0
animateFrameEnd: 9
animateFramePingPong: false
animateFrameSpeed: 0.2
animateFrameSpeedRandom: 0.02
dirOffsetRandom: 360
xOffsetRelativeRandom: 31
yOffsetRelativeRandom: 31

[effect_痕迹]
image: scorchmark.png
life:600
lifeRandom: 100
fadeOut:true
attachedToUnit:false
scaleFrom: 1.1
scaleTo: 1.1
alpha: 0.7
drawUnderUnits:true
attachedToUnit:false
fadeInTime:3
dirOffsetRandom: 8
priority: low

[effect_爆炸烟雾]
scaleFrom: 1.8
scaleTo: 4.3
alpha: 0.78
drawUnderUnits:false
liveAfterAttachedDies:false
hSpeed:0.4
hSpeedRandom: 0.08
dirOffsetRandom:360
ySpeedRelative: 0.2
xSpeedRelativeRandom:0.26
ySpeedRelativeRandom: 0.1
xOffsetRelativeRandom:12
yOffsetRelativeRandom:12
atmospheric:true
life: 400
lifeRandom: 100
fadeOut:true
fadeInTime:4
attachedToUnit:false
image: blackSmoke1.png
dirSpeedRandom: 0.82
alsoPlaySound:Gorgon missile explosion.wav:0.44

[effect_shotMark]
attachedToUnit:false
life:200
physics:false
image:craterBig.png
hOffset:1
priority:critical
createWhenOverLiquid:false
alwayStartDirAtZero:true
fadeInTime:50
scaleFrom:1.2
scaleTo:1.2
alpha:3
drawUnderUnits:true

[effect_projectileGroundSplash]
image:sub_bubbles.png
createWhenOverLiquid:false
life:120
fadeOut:true
attachedToUnit:false
color:#463126
fadeInTime:5
scaleFrom:2
scaleTo:6
alpha:1
drawUnderUnits:false
hSpeed:1
hOffsetRandom:0.3
dirOffsetRandom:180
physics:true
physicsGravity:0.1
xOffsetRelativeRandom:16
yOffsetRelativeRandom:16
xSpeedAbsoluteRandom:0.8
ySpeedAbsoluteRandom:0.8
atmospheric:true
[effect_projectileWaterSmoke]
stripIndex:effects
frameIndex:0
createWhenOverLand:false
life:360
fadeOut:true
attachedToUnit:false
color:#FFFFFF
fadeInTime:5
scaleFrom:1.5
scaleTo:10
alpha:0.8
drawUnderUnits:false
hSpeed:0.2
hOffsetRandom:0.15
dirOffsetRandom:180
shadow:true
xOffsetRelativeRandom:32
yOffsetRelativeRandom:32
xSpeedAbsoluteRandom:0.3
ySpeedAbsoluteRandom:0.3
atmospheric:true
[effect_projectileWaterSplash]
image:sub_bubbles.png
createWhenOverLand:false
life:120
fadeOut:true
attachedToUnit:false
color:#FFFFFF
fadeInTime:5
scaleFrom:2
scaleTo:6
alpha:1
drawUnderUnits:false
hSpeed:1
hOffsetRandom:0.3
dirOffsetRandom:180
physics:true
physicsGravity:0.1
xOffsetRelativeRandom:16
yOffsetRelativeRandom:16
xSpeedAbsoluteRandom:0.8
ySpeedAbsoluteRandom:0.8
atmospheric:true

