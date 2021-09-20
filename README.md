# Optimization based Tight Maneuvering around Moving obstacles for Collision avoidance and Lane Tracking using CASADI

In this repository, I implemented an Optimization based Model predictive control algorithm to perform Tight Maneuvering around Moving Obstacles for collision avoidance while tracking the given lane and reaching the goal location. The objective is to find directly the control actions i.e. the steering rate, jerk rate and the control time step by solving one optimization problem such that the ego vehicle navigates smoothly around the close proximities of the surrounding moving obstacles, without violating other constraints like road boundaries, Wheel lift-off Vertical loads for rollover safety from Longitudinal/Lateral weight transfer, the actuator limits and maintaining a constant preview distance at all times until and unless the ego vehicle is very close to the goal location. Similar problem was also solved in one of my previous attempt in [6] where the collision avoidance constraints are formulated such that the entire predicted trajectory of the ego vehicle remain out of a certain elliptical region around the most nearest identified points from the bounding box of the moving obstacles and the discretesized road boundaries. Since the vehicles are rectangular and not elliptical in shapes, this constraint formulation hinders the ability of the vehicle to tightly maneuver around the moving obstacles impeding the overall navigation of the ego vehicle as was also observed in the results of my previous implementation [6]. Also, considering a vehicle as an ellipsoid can be very conservative and will prevent the car from navigating around the close proximities of the vehicle. To alleviate this issue, Zhang et al. [3] proposed to model the full dimensional shapes of the vehicles as polytopic sets and formulated the collision avoidance constraints non-conservatively as a function of distance between these sets. The distance function is appropriately reformulated using the strong duality of convex optimization resulting in smooth nonlinear constraint functions which can be handled efficiently by any standard nonlinear solvers [5]. I therefore changed my previous repository and implemented these reformulated smooth collision avoidance constraints using CASADI to revalidate its effectiveness for the above mentioned scenario. Other ideas of fusing of Moving obstacle states, Vehicle Dynamic model, objective function, maintaining a constant preview distance and vehicle dynamic rollover safety constraints in the NMPC formulation are still from A.B. Dudekula [1] and is as explained in my previous paper [6]. With the below results, I show the effectiveness of these reformulated smooth collision avoidance constraints to achieve Integrated Path Planning for Tight collision free maneuvering around Moving obstacles and Tracking of the given Lane waypoints for Autonomous navigation in the Highway Structured environment.

![Scenario_Tight_Evasive_Maneuvering (1)](https://user-images.githubusercontent.com/83720464/133929089-5e1322fe-6eae-4c4f-84af-d7924ded9812.gif)

![Results_States_Controls](https://user-images.githubusercontent.com/83720464/133926028-5e4cc311-ea32-4462-ac36-17d03bf06447.png)

# REFERENCES
1.	A.B. Dudekula, Sensor fusion and Non-linear NMPC controller development studies for Intelligent Autonomous vehicular systems, Thesis.
2.	Reza N. Jazar, Advanced Vehicle Dynamics, Springer Book. 
3.	A. L., Xiaojing Zhang and F. Borrelli, Optimization-based collision avoidance, arXiv, 2017.
4.	S. Boyd and L. Vandenberghe. Convex Optimization. Cambridge University Press, 2004. 
5.	R. Firoozi, Xiaojing Zhang and F. Borrelli, Formation and Reconfiguration of Tight Multi-Lane Platoon, arXiv, 2020
6.	M. Saxena, Integrated Path Planning and Control for Lane Tracking with Moving obstacle avoidance. https://github.com/saxenam06/Integrated_Planning_Control_NMPC_CASADI/blob/main/Paper_Integrated_Planning_and_Control_for_Lane_Tracking_V1.pdf
