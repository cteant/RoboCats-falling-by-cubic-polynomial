import numpy as np
def f(n,a,b):
	return np.power(n,3)-300*np.power(n,2)+a*n+b;

def Egg(egg,floor):
	# dynamic programming to compute the number of experiments in the worst case, given the number of egg and floor
	egg_flag = [[0 for x in range(0,floor+1)] for y in range(0,egg+1)];#table to store the results

	# for the first and the zero floor, we will return 1 and 0 respectively
	for x in range(1,egg+1):
		egg_flag[x][1]=1;
		egg_flag[x][0]=0;

	# if there are only one egg, retrun the number of floor
	for x in range(1,floor+1):
		egg_flag[1][x]=x;
		#egg_flag[0][x]=1;
	for x in range(2,egg+1):
		for y in range(2,floor+1):
			egg_flag[x][y] = 65535;
			for v in range(1,y+1):
				temp = 1+max(egg_flag[x-1][v-1],egg_flag[x][y-v]);
				if egg_flag[x][y]>temp:
					egg_flag[x][y]=temp;
	#result=egg_flag[int(egg)][int(floor)];
	#return result;
	return egg_flag

# construct the table with 4 eggs and 200 floors
egg_flag = Egg(4,200);

# algorithm to find the critical floor
def Search(egg,floor,L,a,b,offset=0,reverse=1,time=1,x_last=0):
	#print x_last,L
	#f_last=f(x_last+offset,a,b);

	#if we have only one egg, we have no choice but to test the floor from the bottom to the top floor
	if egg==1:
		x=x_last+1;
	else:
		x=x_last+egg_flag[egg-1].index(L);
	
	#do the experiments
	while x<=floor and round(f(x+offset,a,b),5)*reverse<0 and L>0:
		#print f(x+offset,a,b),x+offset
		time=time+1;
		L=L-1;
		x_last=x;
		x=x+egg_flag[egg-1].index(L) if egg!=1 else x+1;

	if L==0 or egg==1 or abs(f(x+offset,a,b))<1e-5:
		return int(x)+offset, int(time)
	else:
		return Search(egg-1,floor,L,a,b,offset,reverse,time,x_last)

if __name__ == "__main__":
	#randomly generate two integer as the solution
	n1=np.random.randint(low=1,high=280);
	n2=np.random.randint(low=1,high=300-n1);
	n1=91;n2=103
	#n1=15;
	#n2=70;

	#solve the linear equation to obtain a and b
	try:
		[a,b]=np.linalg.solve(np.array([[n1,1],[n2,1]]),np.array([300*np.power(n1,2)-np.power(n1,3),300*np.power(n2,2)-np.power(n2,3)]));
	except np.linalg.linalg.LinAlgError:
		pass
	n = np.roots([1,-300,a,b]);
	print("The roots are", n)
	
	x=100
	time=1

	reverse=-1;
	if f(x,a,b)<=0:
		len_interval=200;
		L=egg_flag[4][len_interval];#four robocats to find n3
		offset=100;
		n_3,t = Search(4,len_interval,L,a,b,offset)
		print("compute n3 = %d in %d experiments"% (n_3,t))
		time=time+t;
		#n3=max(n);
		average=np.round((300-n_3)/2);
		print('average of n1 and n2 is %d' % average)
		if average>=50:
			len_interval=100-average;
			L=egg_flag[3][len_interval];
			n_2,t = Search(3,len_interval,L,a,b,average,reverse);
			print("compute n2 = %d in %d experiments " % (n_2,t))
			time=time+t;
		else:
			len_interval=average;
			L=egg_flag[3][len_interval];
			n_1,t = Search(3,len_interval,L,a,b);
			print("compute n1 = %d in %d experiments " % (n_1,t))
			time=time+t;
	else:
		len_interval=100;
		L=egg_flag[3][len_interval];#three robocats to find n1
		n_1,t = Search(3,len_interval,L,a,b)
		print("compute n1 = %d in %d experiments " % (n_1,t))
		time=time+t;
		
		average=np.round((300-n_1)/2);
		print('average of n2 and n3 is %d' % average)
		if average>=150:
			len_interval=200-average;
			L=egg_flag[3][len_interval];
			n_3,t = Search(3,len_interval,L,a,b,average);
			print("compute n3 = %d in %d experiments"% (n_3,t))
                	time=time+t;
        	else:
			len_interval=average-100;
			L=egg_flag[3][len_interval];
			n_2,t = Search(3,len_interval,L,a,b,100,reverse);
			print("compute n2 = %d in %d experiments " % (n_2,t))
                	time=time+t;
	
	print("The total number of experiments: %d" % time)
