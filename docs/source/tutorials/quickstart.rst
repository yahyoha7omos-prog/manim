from manim import *
import numpy as np

class InfinityCurve(Scene):
    def construct(self):

        # خلفية سوداء
        self.camera.background_color = BLACK

        # عنوان
        title = Text("Integration", color=WHITE).scale(0.8)
        title.to_edge(UP)

        # منحنى اللانهاية ∞
        curve = ParametricFunction(
            lambda t: np.array([
                np.sin(t),
                np.sin(2*t)/2,
                0
            ]),
            t_range=[0, TAU],
            color=GOLD
        ).scale(3)

        # نقطة متحركة
        dot = Dot(color=WHITE).move_to(curve.get_start())

        # سهم
        arrow = Arrow(
            start=LEFT,
            end=RIGHT,
            buff=0,
            color=WHITE
        ).scale(0.5)

        # يخلي النقطة تمشي على المنحنى
        self.play(
            Create(curve),
            run_time=5
        )

        self.add(dot)

        self.play(
            MoveAlongPath(dot, curve),
            Rotate(arrow, angle=PI*2),
            run_time=6,
            rate_func=linear
        )

        self.play(FadeIn(title))

        self.wait()                                    
