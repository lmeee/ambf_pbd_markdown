# ambf_pbd_markdown
# weekly track

## Fall 2021 Nov 4 to Nov 11
  - DiffPBD + DiffCollision: generalize a trajectory by ourselves and combine with diffcol opimizer.
  - DiffPBD + momentum and energy conservation: Rigid body need to be stable in a long simualtion? don't lose energy and add constraint!
  - DiffPBD + force calculation: estimate force exerted to endeffector and 
  - Faster DiffPBD: wrap up some function? switch to cppad or tiny differential simulator?

## Summer 2021 July 4 to July 11
  - Finish matrix version Baxter Arm forward simulation. Compare to previous version, the forward simulation using matrix is 7 times faster than normal forward simulation. Below is an image comparing the time consumption when running 10 time steps forward simulation.
  - ![Screenshot 2021-08-11 05:25:40](https://user-images.githubusercontent.com/51052629/129028292-b50b6c1a-0e4e-4f24-b428-f2a2d9c49f04.png)
  - Able to run the forward for larger time step. Video show the forward simulation for arm falling case when number of time step is 200
  - https://drive.google.com/file/d/1JHsANdV3ufY8y2VDXgYETS5cTYfsFMsW/view?usp=sharing
  - Below is the old version of forward simulation with fewer time steps.
  - https://drive.google.com/file/d/1Ugt9q9UnNSlRIGeL3RQozm9XisUl6l3a/view?usp=sharing



## Summer 2021 July 20 to July 26
  - Finish Baxter left arm simulation with gravity force. Link is below.
  - https://drive.google.com/file/d/1_K68tVc1nTwRBWBuUd9JdCBI2QXVULnW/view?usp=sharing
  - https://drive.google.com/file/d/1Ugt9q9UnNSlRIGeL3RQozm9XisUl6l3a/view?usp=sharing
  - 

## Summer 2021 July 13 to July 19
  - Work on forward simulation of baxter left arm. First translate positional and angular information of joint and arms in URDF file to global frame. Also input the kinematics parameter like mass and inertia tensor into the program. 
  - During forward simulation, joint constraint for hinge joint with the following axis did not converge and error even diverge as the constraint solve carries on. hinge joint about other two axis work well.
  - Fig 1 joint type that is not solved
  - ![gettyimages-73016742-612x612](https://user-images.githubusercontent.com/51052629/126494707-741942db-0684-4ef1-a98d-0e0e6bf1887a.jpg)
  - Fig 2 constraint solve not converge
  - ![Screenshot 2021-07-21 06:01:56](https://user-images.githubusercontent.com/51052629/126492851-db3c689e-ed8e-4789-94c4-066f0c6156d2.png)
  - Fig 3 Image of baxter robot arm in rviz
  - ![Screenshot 2021-07-21 06:40:36](https://user-images.githubusercontent.com/51052629/126498628-aec519cc-8662-4d01-93f0-724347f612eb.png)
 


## Summer 2021 July 6 to July 12
  - finish two hinge joint optimization. True state set to be both robot arm with length 2m. Optimization started with both arm length to be \[1.5m, 1.5m\]. The trajectory, linear velocity and linear acceleration on z-axis at each PBD iteration is recorded and compute loss with the true state. loss drop from 9.68 to 0.147 with final optimized arm length to be \[2.08, 1.85\]. Video comparison is attached.
  - true state with arm length \[2.,2.\]: https://drive.google.com/file/d/1d8l_6H8bIbZh_tKepiPuxSaF_3S35Cwn/view?usp=sharing
  - optimized state arm length \[2.08, 1.85\]: https://drive.google.com/file/d/1uwOPLpz88X4XmYAqBf_w3Xzo6QS7CpUY/view?usp=sharing
  - optimization process (using ADAM):
  - ![gradient](https://user-images.githubusercontent.com/51052629/125592536-284f1036-2d56-4d48-8776-8316a8982eee.png)

  - converting code from cpp to python, currently forward simulation for one hinge work, but for autograd with pytorch, the following problem met.
  - ![Screenshot from 2021-07-09 19-56-55](https://user-images.githubusercontent.com/51052629/125149816-19874380-e0f0-11eb-9252-d5e1d9bc6f66.png)


## Summer 2021 June 29 to July 5
  - debug on double pendulum, add output expression into the code to provide debug information, the problem seems to be in solvePositionConstraint in the constraint solving iteration. The program could converge when only calculating one hinge joint constraint or calculating hinge joint constraint on seperate single pendulum case (joint1.solvePositionConstraint(rblist[0], rblist[1]);joint2.solvePositionConstraint(**rblist[0]**, rblist[2])) but explore to nan when calculating regular consecutive pendulum case (joint1.solvePositionConstraint(rblist[0], rblist[1]);joint2.solvePositionConstraint(**rblist[1]**, rblist[2]));
  - Single pendulum demo done, true pendulum length set to be 2m and initial estimated pendulum length set to be 1, optimized with GD with 100 steps, final estimated pendulum length is 1.9930m.
  - ![Screenshot 2021-06-30 14:47:10](https://user-images.githubusercontent.com/51052629/124036123-5f3a6280-d9b2-11eb-87e1-0edbb87dbb12.png)




## Summer 2021 June 21 to June 28
  - finish template structure for DiffPBD, currently debugging the code. For regular case where data type being float (normal simulation), the code works. But for data type being CPP::AD<float> which is used for operation sequence recording, the code did not work. Main reason is that some eigen operation did not support cppad, need to rewrite it into correct format.


## Summer 2021 June 14 to June 20
  - cmake configuration finish and loss function, simulation part finish, now writing the cppad differentiation part, original code is complicated with specification on different algebra and differentiation method and need to extract cppad out only. currently deal with cppad AD type variable error in cppad.
  - ![Screenshot 2021-06-23 10:21:25](https://user-images.githubusercontent.com/51052629/123141097-dbf69b00-d40c-11eb-82a1-9dec578bd0c0.png)



## Summer 2021 June 8 to June 13
  - migrate cppad differentiation code part from tiny diff to DiffPBD due to error in executing PBD in tiny diff. 
  - Problems in executing cppad in DiffPBD, make error with make, executabel file generated but make error exist.
  -  ![image](https://user-images.githubusercontent.com/51052629/122255436-f5cf3580-ce82-11eb-9210-91801734cd35.png)


## Spring 2021, Week 9-10 May 24th to June 8th

  - final exam and projects
  - 


## Spring 2021, Week 8 May 17th to May 23th
  - implement single hinge joint differential simulation differentiate with respect to pendulum length using tiny simulator based on CPPAD.
  - Scene include one hinge joint (1 dof). We predefine a ground truth simulation with a set link length (say length is 2), the trajectory is collected (position, velocity, acceleration). Then for each simulation with different link length, we can collect the trajectory and calculate the loss function (say norm of difference between trajectory and ground truth). Then we get a loss function with input link length and output error of current simulation. Then we initialize a link length (say link length is 1) and update link length based on the gradient descent and find optimal value. 
  - take pendulum_sys_id.cpp as sample, add my PBD simulation as third_party project and switch the simulation in original file to PBD.
  - code can be executed now, but gradient is not computed correctly. Also, when input is not changing, the cost change.
  - ![image](https://user-images.githubusercontent.com/51052629/119650324-88c30580-bdd8-11eb-9dfb-fde9e0d38724.png)
  - gradient is always 0. configuration of cppad is not correct or problem in rollout function?


## Spring 2021, Week 7 May 10th to May 16th
  - take a vaccine shot.
  - executable added for the demo in tiny simulator. understand the procedure of how the simulation is run and how the gradient is computed.
  - The demo use cppad jacobean to compute the gradient for Gradietn descent method.
  - Still have some problems on how the GradientFunctional class interact with class simulation and cppad.
  - 1, How simulation pass the rollout function to GradientFunctional
  - ![Screenshot from 2021-05-19 04-16-58](https://user-images.githubusercontent.com/51052629/118804444-8bae7b00-b859-11eb-8036-0d1d087a7050.png)


## Spring 2021, Week 5&6 April 26th to May 10th
  - code reading, find a demo that could be useful for implementing diff framework. pendulum_sys_id.cpp has a application that optimize an input parameter link length of pendulum by differentiating with cppad. The ground truth is based on simulation produced with link_length=1.5. The initial guess for optimization is set to be link_length=1.
  - If this demo is good, will start writing my code for diff pbd based on it.



  - paper reading for collision differential framework
    -  1, IPC (ultimate goal, complex deformable body contact solving) https://zhuanlan.zhihu.com/p/154542103
    -  2, ADD
    -  3, diff DART stanford
    -  4, NeuralSim (https://github.com/google-research/tiny-differentiable-simulator) current major work also read the paper, try the code
  
  - pipeline:
    - 1, PBD framwork
    - 2, collision solver (start with easy, try complicate the scene, ex bump ground, simulate with triangle mesh, diff dart paper mention it)
    - 3, make it differential (diff engine in stanford paper)
    - 4, fun control problem, para estimation


  - complie and run https://github.com/google-research/tiny-differentiable-simulator . The project is successfully complie, still looking into how the make visualization work. Currently the meshcat visualizer only display empty scene.
  - ![Screenshot 2021-05-05 02:49:48](https://user-images.githubusercontent.com/51052629/117124080-b9210200-ad4c-11eb-9e5f-4e6556fbc6a4.png)



## Spring 2021, Week 4 April 19th to Apr 25th
  - paper reading.
  - An collision demonstration between cube and ground. (https://drive.google.com/file/d/1GeY8Tnkrtcw5uCQ4YiW2lXRtjfFOfCNB/view?usp=sharing) But did not add this constraint to the 2 dof robot now.
  - Sadly, current demo is not good. Should focus on thinking about the solver's idea and paper reading. 


## Spring 2021, Week 3 April 12th to Apr 18th

  - learn about differential physics simulation from Nvidia forum.
  - implement the 2D collision PBD and making Sample demo， currently no good demo.
  - Question: what kind of rigid body solver we are going to implement, what information it could output?
  
## Spring 2021, Week 2 April 5th to Apr 11th
  - visualization of Forward Dynamics of Planar 2-DOF Robot Manipulator (https://www.mathworks.com/matlabcentral/fileexchange/69756-forward-dynamics-of-planar-2-dof-robot-manipulator)
  - https://drive.google.com/file/d/1MzpMO7FhU3oKKVKPscgNdMQZPtWrjUgf/view?usp=sharing
  - trying to figure out what is the problem and improve algorithm
  - Dealing with contact, create a simulation between a cube and the ground with the collision constraint and the cube should not penatrate the ground.
  - link is : https://drive.google.com/file/d/167NacII0xv5_3oA5zz2VbL3Wu2v8Wsnt/view?usp=sharing
  - the left cube had the collision constraint and the right one does not have. Thus, the left one stay on the ground and the right one falls.
  - question: redering problem, inertia modelling, 2d collision implementation, future works on diffdart

## Spring 2021, Week 1, Mar 29th to Apr 4th
  - find out why is PBD sim and largrange sim different
  - PBD sim weird movement frame num: 43-48, see details about this frame.
  - compare with 2 hinge joint PBD sim created by PositionBasedDynamics project
  - PBD demo problem found, the second joint angle calculation is wrong (just use pose of the second link in the world frame). The correct way was to view the second link in the frame of the first link. Now it is correct.
  - https://drive.google.com/file/d/1EajYWE59kECohwiEI5NlxcN3HUoRH4YI/view?usp=sharing
  - this one seems to be correct.
  - ![屏幕截图(2)](https://user-images.githubusercontent.com/51052629/113382542-8f804f80-9336-11eb-9ad0-ae0273df6128.png)
  - Writing report about PBD and Euler-Largrange performance and their analysis.


## Winter 2020, Spring break Mar 22nd to Mar 28th
  ## two hinge ur robot pbd
  - video of PBD (two hinge joints) with universal robots' viusal links with vertical gravity only.
  - https://drive.google.com/file/d/13K7LCcCuszDuSii1sAU0SuGWMVRAT3JR/view?usp=sharing
  - q1 is the first joint angle and q2 is the second joint angle
  - ![untitled2](https://user-images.githubusercontent.com/51052629/113106433-a0568700-91b7-11eb-8f72-0ad3e27ae860.jpg)

  - strange movement of second link, need more investigation on poses of two links in each frames 
  ## dynamic model of two hinge ur robot
  - Read and understand 2R robot dynamics model (Euler Largrange method, energy based method)
  - ![image](https://user-images.githubusercontent.com/51052629/112834150-7f255780-904c-11eb-86b7-8eb1e09e925e.png)
  - questions about solving differetial equation of dynamic model (2R robot), what method I can use for solving ODE with 2 unknown function? (unknown is q1, q2 and their derivative, others are known)
  - solve the ode and do visualization.
  - ![image](https://user-images.githubusercontent.com/51052629/113099285-911f0b80-91ae-11eb-83b3-bbe7ffefad8f.png)
  - q1 is the first joint angle and q2 is the second joint angle
  - ![untitled2](https://user-images.githubusercontent.com/51052629/113107175-79e51b80-91b8-11eb-9141-ce3f846b0e0d.jpg)

  - plotting of the result show that the robot total energy is increasing, and finally it will rotate in circle instead of oscillating, so does the demo video.
  - https://drive.google.com/file/d/1-nNLb-RdzsB4hSp8oLtvkjrCDCVKYGMH/view?usp=sharing

----------------------------------------------------------------------------------------------------------------------------------------

  - video of PBD single hinge joint with universal robots' viusal links with gravity only. Control the joint angle with a publisher subscribed to '/joint_states'
  - https://drive.google.com/file/d/1kIHEau3ELO2WacyncHx09XrSdKeCnqqH/view?usp=sharing
  - take delta_x = 0.05s, try h = 0.001s/0.005s/0.01s (num of step = 50/10/5), smaller the h, larger the height when arm can reach when swinging to the other side. 
  - ![urdf](https://user-images.githubusercontent.com/51052629/112269111-2a8d7100-8c35-11eb-8e5f-9bd9d563d5fb.png)

  - Another simulation with a higher starting points:
  - https://drive.google.com/file/d/1I1KV2TUsMAn3cZRrr3-dyrqhi6cQz8Je/view?usp=sharing
  - Another simulation with a highest starting points:
  - https://drive.google.com/file/d/1Lwvol186Mt0vXgxynf45DrFdeS13NfCM/view?usp=sharing
  - FORMER DEMO has gravity (2.0, 10.0, 0.0) in pbd
  - Another simulation with a highest starting points (vertical gravity):
  - https://drive.google.com/file/d/1Lq0pbeiK9Ecvs6i2zw6cNFyHBHI2bmAN/view?usp=sharing




  - highest radian it could reach 0.001s: 3.12763rad, 0.005s: 3.06064rad, 0.01s: 2.98691rad
  - Next step: add another hinge joint, create comparison with 2D dynamic model


## Winter 2020, Week 10 Mar 15th to Mar 21st 
  - goal: implement ur5 model with 2 hingejoints, complete visualization and compare it with the Newton-euler implementation.

  - Work on friction simulation, complete a basic structure for it.
  - A simple visualization program by communicating with publisher in ROS rviz to move robot. 

## Winter 2020, Week 6 Mar 8st to Mar 14th 

  - It is final week, prepare for exam and project
  - position constraint only simulation (totally 60 frames, interval: 0.05s, each screen every 3 frames take one screenshot for gif )
  - gravity is along -y axis, [0, 10, 0]
  - ![pos](https://user-images.githubusercontent.com/51052629/110712337-e078aa00-81b5-11eb-8fb8-8815c6766713.gif)


  - position constraint an d angular constraint together for hinge joint. To test angular constraint, we add and offset to gravity to let angular constraint adjust according to hinge joint constraint.
  - gravity [2, -10, 0]
  - ![ang](https://user-images.githubusercontent.com/51052629/110713201-5bda5b80-81b6-11eb-83ab-f855d4b42a5b.gif)

  - screenshot of an urdf file of second case
  - In second link, hinge joint will have rpy to be approximately [r_value, 0, 0] with the x axis to be aligned. In the sample urdf, <origin rpy="2.09e+00 1.43e-03 1.10e-03" xyz="1.61e-03 -1.12e+00 -4.97e-01"/>. angular constraint modified the value
  - without angular constraint (not hinge joint)
  - ![3posnoang](https://user-images.githubusercontent.com/51052629/110714451-3e0df600-81b8-11eb-80a2-fcc471761379.png)
  - with angular constraint (hinge joint)
  - ![3ang](https://user-images.githubusercontent.com/51052629/110714452-40705000-81b8-11eb-93d0-4007afc0ac57.png)




## Winter 2020, Week 6 Mar 1st to Mar 7th

  - learn about hinge solver in code and learn about quaternion.
  - implement positional constraint and angular constraint for hinge joint with XPBD
  - solver perform well in first 9 frame, but diverge in some specific case.

  - gif
  ![test](https://user-images.githubusercontent.com/51052629/110669297-0b94d680-8181-11eb-9376-ed1e800779cc.gif)
  - in 10th frame step, solver perform well in beginning step but diverge in the following. In normal case, the vector n(n is the delta x before normalizing) should decrease to a value close to 0 in the process 
  - this cause a large velocity is recorded and use in 11th frame step and result in a large vector n in the first iteration.
  ![Screenshot from 2021-03-09 20-00-48](https://user-images.githubusercontent.com/51052629/110574563-2ed46d00-8112-11eb-8dc2-b9bb66e975ae.png)

  frame 9
  ![Screenshot from 2021-03-08 04-55-05](https://user-images.githubusercontent.com/51052629/110573971-14e65a80-8111-11eb-86ba-43e9d68b8503.png)

  frame 10
  ![Screenshot from 2021-03-08 04-53-47](https://user-images.githubusercontent.com/51052629/110573937-05671180-8111-11eb-9418-8259ecb6efcb.png)
  
  frame 11
  ![Screenshot from 2021-03-08 04-54-03](https://user-images.githubusercontent.com/51052629/110573953-0d26b600-8111-11eb-8c48-95b6ec72ebcb.png)




## Winter 2020, Week 6 Feb 22 to Feb 28
- Goal: Write rigid body PBD with joint constraint (universal constraint and slider constraint) with extend PBD

  - Rigid body class
  - Universal constraint implementation
  - A simulation with 2 rigid bodies connected with universal joint
  - Visualization for every time step with URDF file and ROS rviz
  - Understanding XPBD
  - t = 0*0.05s
  ![image](https://user-images.githubusercontent.com/51052629/109461780-84748f80-7a17-11eb-9c4f-a7482fa8734b.png)

  - t = 30*0.05s
  ![image](https://user-images.githubusercontent.com/51052629/109461872-a241f480-7a17-11eb-84f1-ffee9de73be8.png)


## Winter 2020, Week 6 Feb 15 to Feb 21
- Goal: write method and members for pbd physics which replace cBulletWorld class

  - change cmakelist to include source files
  - construct header file example.h.
  - write example.cpp, an example of a cuboid which is pulled by a constanst external force.
  - apply shapematching constraint and met unstable output.
  - output example
  ```
  iteration #9
  9 th iteration: final position for particle 0 : 1.390e-309 | 7.245e-183 | 1.375e+01 
  9 th iteration: final position for particle 1 : 1.000e+00 | 7.245e-183 | 1.375e+01 
  9 th iteration: final position for particle 2 : 1.000e+00 | 1.000e+00 | 1.375e+01 
  9 th iteration: final position for particle 3 : 1.390e-309 | 1.000e+00 | 1.375e+01 
  9 th iteration: final position for particle 4 : 1.390e-309 | 7.245e-183 | 1.475e+01 
  9 th iteration: final position for particle 5 : 1.000e+00 | 7.245e-183 | 1.475e+01 
  9 th iteration: final position for particle 6 : 1.000e+00 | 1.000e+00 | 1.475e+01 
  9 th iteration: final position for particle 7 : 1.390e-309 | 1.000e+00 | 1.475e+01
  ```
  
  TODO:
    - OOP, divide into classes
    - more constraints
    - visualization
    - import robots (joint constraints)



## Winter 2020, Week 6 Feb 8 to Feb 14

- Goal: create a simple simulation (ex. A bunch of particles) in ambf with PBD. change the physics simulation from BULLET-PHYSICS to PBD. Replace cBulletWorld class with my pbd class. Rewrite method and members in it. 


- Understand from ambf_simulator.cpp, this code create dynamic world (bullet world) 
  ```
  g_afWorld = new afWorld(g_cmdOpts.prepend_namespace);
  ```
  - type Afworld inherited from public cBulletWorld, public afConfigHandler, public afComm
  
- Members in cBulletWorld class:
  - btDiscreteDynamicsWorld
    ```
    //! Bullet dynamics world.
    btDiscreteDynamicsWorld* m_bulletWorld;
    ```
    - btDiscreteDynamicsWorld->btDynamicsWorld->btCollisionWorld
    - Add or remove constraint in line 1100 in afFramework.cpp
    - stepSimulation

  - btBroadphaseInterface
    ```
    //! Bullet broad phase collision detection algorithm.
    btBroadphaseInterface* m_bulletBroadphase; (btBroadphaseInterface.h)
    ```
    - In cBulletWorld

  - btCollisionConfiguration
    ```
    //! Bullet collision configuration.
    btCollisionConfiguration* m_bulletCollisionConfiguration; (btCollisionConfiguration.h)
    ```
    - In cBulletWorld

  - btCollisionDispatcher
    ```
    //! Bullet collision dispatcher.
    btCollisionDispatcher* m_bulletCollisionDispatcher;
    ```
    - btCollisionDispatcher->btDispatcher
    - In cBulletWorld

  - btConstraintSolver
    ```
    //! Bullet physics solver.
    btConstraintSolver* m_bulletSolver;
    ```
    - Q: No cpp file found for this?
    - In cBulletWorld

  - not consider for now
    ```
    //! Bullet Softbody World Info
    btSoftBodyWorldInfo* m_bulletSoftBodyWorldInfo;
    //! Bullet Soft Body Solver
    btSoftBodySolver* m_bulletSoftBodySolver;
    ```

- final goal: PBD framework with
  - rigid body (simulated as a point in previous work) and deformable body, interaction between rigid and deformable bodies (friction, etc).
  - ROS
  - haptics力反馈
  - differentiable

