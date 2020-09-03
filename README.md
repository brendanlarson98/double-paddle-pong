# double-paddle-pong
## This will make a cooler game of pong
### We first need to import python's turtle module

    import turtle
### We then need to make our Turtles
#### First we creat our screen, sized 800x600 pixels. We set a delay and tracer to keep our game from running too fast.
    screen = turtle.Screen()
    screen.setup(800, 600)
    screen.bgcolor("black")
    screen.delay(10)
    screen.tracer(0)
    screen.update()
#### Next we create our respective paddles. Normally Turtles leave a trail behind, the up() function gets rid of that.
    far_l_paddle = turtle.Turtle()
    far_l_paddle.shape("square")
    far_l_paddle.up()
    far_l_paddle.color("purple")
    far_l_paddle.speed(0)
    far_l_paddle.shapesize(stretch_len=1, stretch_wid=5)
    far_l_paddle.goto(-350, 0)
    
    far_r_paddle = turtle.Turtle()
    far_r_paddle.shape("square")
    far_r_paddle.up()
    far_r_paddle.color("blue")
    far_r_paddle.speed(0)
    far_r_paddle.shapesize(stretch_len=1, stretch_wid=5)
    far_r_paddle.goto(350, 0)
    
    r_paddle = turtle.Turtle()
    r_paddle.shape("square")
    r_paddle.up()
    r_paddle.color("green")
    r_paddle.speed(0)
    r_paddle.shapesize(stretch_len=1, stretch_wid=5)
    r_paddle.goto(275, 0)
    
    l_paddle = turtle.Turtle()
    l_paddle.shape("square")
    l_paddle.up()
    l_paddle.color("yellow")
    l_paddle.speed(0)
    l_paddle.shapesize(stretch_len=1, stretch_wid=5)
    l_paddle.goto(-275, 0)
#### Our pong ball, which will move in an x and y rate of .15, which should change based on the computer you are running on.
    pong = turtle.Turtle()
    pong.shape("square")
    pong.up()
    pong.speed(1)
    pong.color("red")
    pong.goto(0, 0)
    pong.dx = .15
    pong.dy = .15
#### This is our title, showing the score.
    title = turtle.Turtle()
    title.speed(0)
    title.color("purple")
    title.up()
    title.hideturtle()
    title.goto(0, 260)
    title.write("Player 1: 0   Player 2: 0", align="center", font=("Arial", 20, "normal"))
    
    p1_score = 0
    p2_score = 0
    
### Here we create our functions, which add or subract y value.
    def far_l_up():
        up = far_l_paddle.ycor()
        up += 20
        far_l_paddle.sety(up)
    
    
    def far_l_down():
        down = far_l_paddle.ycor()
        down -= 20
        far_l_paddle.sety(down)
    
    
    def far_r_down():
        down = far_r_paddle.ycor()
        down -= 20
        far_r_paddle.sety(down)
    
    
    def far_r_up():
        up = far_r_paddle.ycor()
        up += 20
        far_r_paddle.sety(up)
    
    
    def r_up():
        up = r_paddle.ycor()
        up += 20
        r_paddle.sety(up)
    
    
    def r_down():
        down = r_paddle.ycor()
        down -= 20
        r_paddle.sety(down)
    
    
    def l_up():
        up = l_paddle.ycor()
        up += 20
        l_paddle.sety(up)
    
    
    def l_down():
        down = l_paddle.ycor()
        down -= 20
        l_paddle.sety(down)
    
### With the turtle onkeypress() function, we assign our y-value functions to respective keys.
    screen.listen()
    screen.onkeypress(far_l_up, "w")
    screen.onkeypress(far_l_down, "s")
    screen.onkeypress(far_r_up, "Up")
    screen.onkeypress(far_r_down, "Down")
    screen.onkeypress(r_up, "/")
    screen.onkeypress(r_down, "Left")
    screen.onkeypress(l_up, "e")
    screen.onkeypress(l_down, "d")
    
### Here we create our main loop.
    while True:
        screen.update()

        pong.setx(pong.xcor() + pong.dx)
        pong.sety(pong.ycor() + pong.dy)
#### These if statements let the ball reverse direction when the ball impacts one of our paddles or the upper and lower wall.
        if (340 < pong.xcor() < 360) and ((far_r_paddle.ycor() - 50) <= pong.ycor() <= (far_r_paddle.ycor() + 50)):
            pong.dx *= -1
    
        if (265 < pong.xcor() < 285) and ((r_paddle.ycor() - 50) <= pong.ycor() <= (r_paddle.ycor() + 50)):
            pong.dx *= -1
    
        if (-360 < pong.xcor() < -340) and ((far_l_paddle.ycor() - 50) <= pong.ycor() <= (far_l_paddle.ycor() + 50)):
            pong.dx *= -1
    
        if (-285 < pong.xcor() < -265) and ((l_paddle.ycor() - 50) <= pong.ycor() <= (l_paddle.ycor() + 50)):
            pong.dx *= -1
    
        if pong.ycor() > 290 or pong.ycor() < -290:
            pong.dy *= -1
#### If the ball leaves either side, we reset its direction and position and add to the score. We clear our title Turtle and rewrite.
        if pong.xcor() > 395:
            pong.setx(0)
            pong.sety(0)
            pong.dx *= -1
            pong.dy *= -1
            p1_score += 1
            title.clear()
            title.write(f"Player A: {p1_score}   Player B: {p2_score}", align="center", font=("Courier", 24, "normal"))
    
        if pong.xcor() < -395:
            pong.setx(0)
            pong.sety(0)
            pong.dx *= -1
            pong.dy *= -1
            p2_score += 1
            title.clear()
            title.write(f"Player 1: {p1_score}   Player 2: {p2_score}", align="center", font=("Arial", 20, "normal"))
#### If the score reaches 5 for either player, they win!!
        if p1_score == 5:
            pong.clear()
            pen = turtle.Turtle()
            pen.speed(0)
            pen.color("white")
            pen.up()
            pen.hideturtle()
            pen.goto(0, 0)
            pen.write("Player 1 wins!!", align="center", font=("Arial", 30, "normal"))
    
        if p2_score == 5:
            pong.clear()
            pen = turtle.Turtle()
            pen.speed(0)
            pen.color("white")
            pen.up()
            pen.hideturtle()
            pen.goto(0, 0)
            pen.write("Player 2 wins!!", align="center", font=("Arial", 30, "normal"))
