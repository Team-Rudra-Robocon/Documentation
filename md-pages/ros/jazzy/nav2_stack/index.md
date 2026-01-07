# NAV2


Nav2 or Navigation 2 consist of behavior trees which help in planning andn controlling the robots autonomously . Basically tells the robot how where and what to do / move. 

The Nav2 stack is built using the following 
1. Mapping 
2. Localisation 
3. Planning
4. Control
5. Recovery


These things are done using Behavior Trees , BTs are basically nodes that tell what to do now? , Navigation system requires the following things 

1. Goal - where to go ?
2. Localisation - where am I right now and how to traverse from where I am ?
3. Costmap - where else can I go in the environment ?
4. Planner - How to get to the goal ?
5. Controller - How to move safety without damage ?


therefore Nav2 is a flugin where everything can be custom made during runtime this helps with research and  helps in custom making robots.