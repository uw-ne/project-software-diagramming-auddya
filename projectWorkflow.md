A coarse architecture for the project is described below:

## Read Input
 
```
def guitar string_input():

	This function is used to define manually the values of the string parameters
	Such as Length of the domain, time length of oscillation, amplitude of pluck, 
	frequency et cetera, Courant number etc. 
	
	Input
	------ 
	- Defines the values as mentioned above within the function
	
	Output
	------
	- The output of this function can be used as input parameters for other functions
	  which involve solving equations using these values. 

```

## Solve Physics 

  #Setup Problem

```
def solving_function_initialisation(guitar string parameters):

	This function is used to define variables and `arrays` which are required to solve the 
	finite difference equation of the elliptic PDE.

	Input
	------
	- guitar string parameters: Initial values (u[x,0], v[x,0]) of the PDE, size of temporal steps,
          size of spatial steps, Courant number, velocity of string etc. 
	- Should also initialise solution arrays
	  
	  eg: Nt = int(round(T/dt))  #Number of temporal nodes
   	       t = np.linspace(0, Nt*dt, Nt+1) #Dividing time into number of equidistant contiguous steps

	       u = np.zeros(Nx + 1) #Solution array at a present time
	     u_1 = np.zeros(Nx + 1) #Solution arrat at time 1 level back etc. 	
		
	Output	
	------		  		 	
	- Solution arrays and other parameters defined above will serve as an input to the next functions

```

  #Loop over First time step

          Working algorithm:
        ------
        - Initially we load our initial condition into u_1 (Solution array at one time level back)
        - Update u with special function that utilised u_1.
        - Switch variables before next step


```
def special_function_for_first_time_step(solution arrays, initial condition, other parameters):

	This function lets us initialise the solution array and solve the equation for the first time step
	We need this step as according to our FD equation, when n = 0, one of the indices have a -1 term in 
	its index which requires some algebraic manipulation to build a new equation only for the first time step

	Input
	------ 
	- solution arrays: Solution arrays for present time and one and two steps behind needed for the simulation
	- initial condition: For t = 0, the condition of the string needs to be stored in the array
	- other parameters: Total number of nodes in spatial domain

	Output
	------
	- Updated u and switched variables as an input for the next function

```
   #Loop over all time steps,solve the problem and update time step
        
	Working algorithm:
        ------
        - Loop over temporal intervals
        - Loop over spatial intervals
        - Apply finite difference formula
        - Insert boundary conditions after each time step
        - Switch variables before next time step

```
def main_function_simulation(arrays, other parameters):
	
	This functions fills up the solution arrays using loops and FD equations

	Input
	------
	- arrays: Arrays from the previous function which will be used in the algorithm
	- other parameters: Needed for the FD equation
	
	Working algorithm:
	------
	- Loop over temporal intervals
	- Loop over spatial intervals
	- Apply finite difference formula 
	- Insert boundary conditions after each time step
	- Switch variables before next time step

	Output
	------
	- Array containing the solution of our problem for a given PDE, IC and BC
```

##Visualise the output

```
def visualisation tools(string parameters, visualisation method, animation modes):
	
	This function is used mainly for viewing the results of our simulation 
	
	Input
	------
	- String parameters: Basic parameters which are needed for defining the values during visualisation.
	- Visualisation method: For python use matplotlib
	- Animate: Since we need to make movies for each time step, we keep this feature ON. 

	Output
	------
	- Visual data which can be analysed 

```
