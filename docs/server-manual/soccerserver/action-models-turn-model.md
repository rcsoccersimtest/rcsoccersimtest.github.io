# Turn Model

While *dash* is used to accelerate the player in direction of its
body, the *turn command* is used to change the players body direction.
The argument for the turn command is the moment; valid values for the
moment are between **server::minmoment** and **server::maxmoment**.
If the player does not move, the moment is equal to the angle the
player will turn. However, there is a concept of inertia that makes it
more difficult to turn when you are moving.
Specifically, the actual angle the player is turned is as follows:

<div align="center">
  ![Field Detailed](./../../../static/img/server-manual/turn_model_eq1.png)
</div>

**server::inertia_moment** is a server.conf parameter with default
value 5.0.
Therefore (with default values), when the player is at speed 1.0, the
*maximum effective* turn he can do is $\pm30$.
However, notice that because you can not dash and turn during the same
cycle, the fastest that a player can be going when executing a turn is
$player\_speed\_max \times player\_decay$, which means the effective turn for a default player
(with default values) is $\pm60$.

<div align="center">
  ![Field Detailed](./../../../static/img/server-manual/turn_model_eq2.png)
</div>

| Default Parameters        | Default Value (Range) | Heterogeneous Player Parameters     | Value |
|--------------------------|-----------------------|-------------------------------------|-------|
| Name                     |                       | Name                                |       |
| server::minmoment        | -180                  |                                     |       |
| server::maxmoment        | 180                   |                                     |       |
| server::inertia_moment   | 5.0 ([2.5, 7.5])     | player::player_decay_delta_min<br></br>player::player_decay_delta_max <br></br>player::inertia_moment_delta_factor      | -0.1<br></br>0.1<br></br>25 |

