# Vectorized-implementation-of-primal-hybrid-FEM-in-MATLAB

Main_PH.m solves the second order elliptic equation with A=I, p=(1,1) and delta=1:
 -nabla.(A nabla u + up)+ delta u = f in (0,1)^2          
u=uD    on the Dirichlet boundary
(A nabla u + up).n = g on the Neumann boundary.


ParabolicMain.m solves the second order parabolic problem with A=I, p=(1,1) and delta=1:           
 d/dt u - div(A nabla u+up)+ delta u =  f  in (0,1)^2,  
  u = u_D                 on the Dirichlet boundary            
(A nabla u+up).n= g      on the Neumann boundary
u0=0                      Initial condition

This Matlab package is developed by N. Harish, K. Porwal, J. Valdman and S. K. Acharya 
(Date: 02/12/2024). It is supplement to the paper "Vectorized implementation of primal hybrid
FEM in MATLAB". The reader should consult that paper for more information.


1. General information on the package

There are three directories when the package is unzipped:

      Edge_Redrefine_StiffMassConvPH_LambdaPH_vectorization
      Mixed_PrimalHybrid(Elliptic)_vectorization-Diff-Conv-React
      Mixed_PrimalHybrid(Parabolic)_vectorization-Diff-Conv-React

[1]. "Vectorized implementation of primal hybrid FEM in MATLAB", N. Harish, K. Porwal, 
      J. Valdman and S. K. Acharya.

The paper [1] presents the overall theory, describes the software package and the examples in detail.



2. Installation Instructions:

i.   Unzip Files:
   - Download and unzip all the files associated with the package.

ii.  Open Matlab:
   - Launch MATLAB on your system.

iii. Set Path:
   - Set the proper path to the directory containing the Matlab modules.
   - This ensures that Matlab can access the required files.

iv.  Run the Package:
   - With the path properly set, the package is now ready to run.



3. Open the directories

i.  Mixed_PrimalHybrid(Elliptic)_vectorization-Diff-Conv-React Directory:
   - Contains Matlab modules for computing the numerical approximation of a second-order elliptic problem.
   - Run "Main.m", which loads mesh data from data-files: <elements.dat>, <coordinates.dat>, <Dirichlet.dat>, <Neumann.dat>.
   - Volume force and boundary data are provided as M-files: <f.m>, <g.m>, <uD.m>.
   - "StiffMassConv_PH.m" computes stiffness, mass, and convection matrices along with the load vector.
   - "Lambda_PH.m" computes the matrix C (Lagrangian multiplier matrix).
   - Uses a reduced linear system of equations in "Main.m" to calculate a discrete solution

ii. Mixed_PrimalHybrid(Parabolic)_vectorization-Diff-Conv-React Directory:
   - Contains Matlab modules for computing the numerical approximation of a second-order parabolic problem.
   - Run "ParabolicMain.m", which loads mesh data similarly.
   - Volume force and boundary data are given as M-files: <f.m>, <g.m>, <uD.m>.
   - "StiffMassConv_PH.m" computes stiffness, mass, and convection matrices.
   - "Lambda_PH.m" computes the matrix C (Lagrangian multiplier matrix).
   - Applies backward Euler explicit method for first-order accuracy in time (h^(r-1)+k, with r=2, h^1 for space, k^1 for time)
   - Applies Crank-Nicolson finite difference scheme for second-order accuracy in time (h^r+k^2, with r=2, h^2 for space, k^2 for time).
   - "load_t.m" computes the load vector and Neumann boundary term LN.
   - Uses a reduced linear system of equations in "ParabolicMain.m" to calculate a discrete solution.



4. Applications

There are four main programs:

  Main.m:                        Calculates the numerical solution of the second-order general elliptic problem 
                                 with mixed boundary conditions. This is based on the lowest-order primal hybrid FEM.
                                 It also calculates the order of convergences with their respective norms listed in Table 4.


  ParabolicMain.m:               Calculates the numerical solution of the general second-order parabolic problem
                                 with mixed boundary conditions. It uses the backward Euler and Crank-Nicolson finite difference 
                                 scheme in the temporal direction, based on the lowest-order primal hybrid FEM. It also calculates the
                                 order of convergences with their respective norms, which is listed in Table 5 (using the backward Euler method) 
                                 and Table 6 (using the Crank-Nicolson method).
 


  MainEdgeRedRefineTesting.m:    Calculates the runtimes listed in Table 2 for the vectorized code of redrefine.m and edge.m.
                                  
 
  MainStiffPHLambdaPHTesting.m:  Calculates the runtimes listed in Table 3 for StiffMassConv_PH.m and Lambda_PH.m.



5. Switch between backward Euler and Crank-Nicolson

In ParabolicMain.m, if we set  

i.     method=1 : we run the Crank-Nicolson method for parabolic problem.

ii.    method=2 : we run the backward Euler method for parabolic problem.


                                 
