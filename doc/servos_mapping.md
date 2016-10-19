# Servos mapping

Servo outputs (in fact, PWMs) are numbered in 3 different ways:

* with a serigraphy on chuck
* with the pwm index in /sys/class/pwm (number to write in the *export* file to
export the pwm)
* with the servo file index in /sys/kernel/hsis/ (servoXpwm)

The following table sums up this mapping:

| serigraphy | hsis file number | pwm index |
| :-:        | :-:              | :-:       |
| 1          | 1                | 4         |
| 2          | 3                | 5         |
| 3          | 5                | 6         |
| 4          | 6                | 1         |
| 5          | 4                | 2         |
| 6          | 2                | 3         |
