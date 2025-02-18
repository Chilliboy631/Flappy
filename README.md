# Flappy

26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70
71
72
73
74
75
76
77
78
79
80
81
82
83
84
85
86
87
88
89
90
91
92
93
94
95
96
97
98
99
100
101
import 'package:flutter/material.dart';
  double gravity = -4.9;
  double velocity = 3.5;
  bool gameStarted = false;
  Timer? gameTimer;

  void startGame() {
    gameStarted = true;
    gameTimer = Timer.periodic(Duration(milliseconds: 50), (timer) {
      setState(() {
        birdY -= gravity * 0.05;
      });
      if (birdY > 1 || birdY < -1) {
        gameTimer?.cancel();
        resetGame();
      }
    });
  }

  void jump() {
    setState(() {
      birdY += velocity * 0.1;
    });
  }

  void resetGame() {
    setState(() {
      birdY = 0;
      gameStarted = false;
    });
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () {
        if (!gameStarted) {
          startGame();
        } else {
          jump();
        }
      },
      child: Scaffold(
        body: Stack(
          children: [
            Container(color: Colors.blue),
            Align(
              alignment: Alignment(0, birdY),
              child: Container(
                width: 50,
                height: 50,
                decoration: BoxDecoration(
                  color: Colors.yellow,
                  shape: BoxShape.circle,
                ),
              ),
            ),
            Positioned(
              top: 50,
              left: MediaQuery.of(context).size.width / 2 - 50,
              child: gameStarted
                  ? SizedBox()
                  : Text(
                      'Tap to Start',
                      style: TextStyle(
                        fontSize: 24,
                        color: Colors.white,
                        fontWeight: FontWeight.bold,
                      ),
                    ),
            ),
          ],
        ),
      ),
    );
  }
}
