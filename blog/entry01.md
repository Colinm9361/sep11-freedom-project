# Entry 1
##### nov/9/26
### Context:
What is my freedom projet about? My freedom project in SEP 11 is about making a new, or similar version to that wifi-less dinosaur game on every computer, using Javascript to code a game. And to support that game, I'll be using Kaboom.js, a website that holds javascript code to create various sorts of simple games.
### Content:
Within this blog, Ill defining what good my project will do, and what is Kaboom.js about in a little more depth. For example:
### Implications:
A tech creation I wish to develop is a similar or an alternative to the wifi-less dinosaur game, to offer an easier accessible wifi-less game for people to play to pass time. Since the dinosaur game is meant as something to pass the time when your computer doesn’t have wifi or internet. Globally, it doesn't do anything regarding education and government, but socially, and through time, it could leave a mark for younger generations. Socially, it could offer as a game to play when bored out of one's mind when the internet isn’t given, and depending on if I make the game multiplayer, may allow for kids or people to play with each other on a split screen. It can offer a new game to play, and leave a lasting mark like how kids nowadays, for if they lose internet connection, will always play and know that dinosaur game. Maybe my game can be another alternative. Economically it’s free, but it could inspire others to want to try making their own games, or test myself to try another game. Overall, though there’s not much the game can do globally, or economically, socially, it can give people something else to play and enjoy outside of paid or wifi reliant games.
### Kaboom.js
The tool I've decided to work on for my game project is Kaboom.js. Kaboom.js is a site that provides various code needed to make simple basic games like: sprites, the code/character that has a function of movement, effects, etc. Code to create a runner, platformer, or RPG game, providing all the basic code needed to create one. Like this code, for making a sprite, showing what animation it's in, and the frames it has:
``` js
// Sprite animation

// Start a kaboom game
kaboom({
	// Scale the whole game up
	scale: 4,
	// Set the default font
	font: "monospace",
})

// Loading a multi-frame sprite
loadSprite("dino", "/examples/sprites/dino.png", {
	// The image contains 9 frames layed out horizontally, slice it into individual frames
	sliceX: 9,
	// Define animations
	anims: {
		"idle": {
			// Starts from frame 0, ends at frame 3
			from: 0,
			to: 3,
			// Frame per second
			speed: 5,
			loop: true,
		},
		"run": {
			from: 4,
			to: 7,
			speed: 10,
			loop: true,
		},
		// This animation only has 1 frame
		"jump": 8,
	},
})

const SPEED = 120
const JUMP_FORCE = 240

setGravity(640)

// Add our player character
const player = add([
	sprite("dino"),
	pos(center()),
	anchor("center"),
	area(),
	body(),
])

// .play is provided by sprite() component, it starts playing the specified animation (the animation information of "idle" is defined above in loadSprite)
player.play("idle")

// Add a platform
add([
	rect(width(), 24),
	area(),
	outline(1),
	pos(0, height() - 24),
	body({ isStatic: true }),
])

// Switch to "idle" or "run" animation when player hits ground
player.onGround(() => {
	if (!isKeyDown("left") && !isKeyDown("right")) {
		player.play("idle")
	} else {
		player.play("run")
	}
})

player.onAnimEnd((anim) => {
	if (anim === "idle") {
		// You can also register an event that runs when certain anim ends
	}
})

onKeyPress("space", () => {
	if (player.isGrounded()) {
		player.jump(JUMP_FORCE)
		player.play("jump")
	}
})

onKeyDown("left", () => {
	player.move(-SPEED, 0)
	player.flipX = true
	// .play() will reset to the first frame of the anim, so we want to make sure it only runs when the current animation is not "run"
	if (player.isGrounded() && player.curAnim() !== "run") {
		player.play("run")
	}
})

onKeyDown("right", () => {
	player.move(SPEED, 0)
	player.flipX = false
	if (player.isGrounded() && player.curAnim() !== "run") {
		player.play("run")
	}
})

;["left", "right"].forEach((key) => {
	onKeyRelease(key, () => {
	// Only reset to "idle" if player is not holding any of these keys
		if (player.isGrounded() && !isKeyDown("left") && !isKeyDown("right")) {
			player.play("idle")
		}
	})
})

const getInfo = () => `
Anim: ${player.curAnim()}
Frame: ${player.frame}
`.trim()

// Add some text to show the current animation
const label = add([
	text(getInfo(), { size: 12 }),
	color(0, 0, 0),
	pos(4),
])

label.onUpdate(() => {
	label.text = getInfo()
})

```

[Next](entry02.md)

[Home](../README.md)