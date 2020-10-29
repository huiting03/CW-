from scipy.integrate import solve_ivp
import numpy as np
import matplotlib.pyplot as plt

# dz/dt = f(t, z)
# t = [0, 1, 2]
# form f(t, z)
# x'= v * cos(θ)
# y'= v * sin(θ)
# θ'=v * tan(u)/L
# state: z = [x, y , θ]
# input: u

v = 5  # 5m/s
L = 2.3  # 2.3m
u = 2. * np.pi / 180.


def system_dynamics(t, z):
   theta = z[2]
   return [v * np.cos(theta), v * np.sin(theta), v * np.tan(u) / L]


t_final = 2
z_initial = [0, 0.3, 0.08]
solution = solve_ivp(system_dynamics, [0, t_final], z_initial,t_eval=np.linspace(0, t_final,100))
x_trajectory =solution.y[0]
y_trajectory =solution.y[1]
theta_trajectory = solution.y[2]

plt.plot(solution.t, theta_trajectory)
plt. show()
