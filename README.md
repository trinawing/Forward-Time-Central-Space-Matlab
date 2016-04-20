# Forward-Time-Central-Space-Matlab

clear all
%%% Trina Wing %%%%%
%%%%%% FTCS %%%%%%%%
h = 1/50;
t = 0;
tf = .8;
mu = 1;
k = mu*h^2;
c = .1;
a = 10;
alpha = (h*a)/(2*c)
T = t:k:tf;
N = length(T);

L = 0; 
R = 1;  
x = L:h:R;
M = length(x);
U = zeros(M,1);


    
 
for j = 1:M

    U(j) = sin(pi*x(j));

end



result = U;
u_old = U;
u_new = U;


for i = 2:N;

    t = t + k;
    u_new(1) = 0;

    for j = 2:M-1

      
u_new(j) = (1-2*c*mu)*u_old(j) + c*mu*(1-alpha)*u_old(j+1) + c*mu*(1+alpha)*u_old(j-1);
       
    end

    

    result = [result u_new];

    u_old = u_new;

  

 if rem(i,56) == 0  

    plot(x,u_new,'-^'), ylim([-2 2]), xlim([0 2]), hold on

    xlabel('x'), ylabel('U'),

    legend('approximate'), title('Soltuion at t = .8'), pause,
 end 

end
