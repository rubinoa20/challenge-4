int l_motor = 0; 
int r_motor = 2;
int forward = 40;
int backward = -35;
int slow = 15;
int left = 50;
int right = -50;
int turn_pause = 450;
int turn_pause_dos = 850;
int turn_pause_tres = 850;
int pause = 1500;
int straight = 12500;
int infared = 5; //right reflectance
int range_front = 1;
int infared_spot = 750;
int f_average = 300;
int f_dos = 750;
int v_speed = 95;


void forwards(){ //go forward
    motor(l_motor,forward);
    motor(r_motor,forward);
}
void turn(){ //turn
	motor(l_motor,left);
    motor(r_motor,right);
	msleep(turn_pause);
	ao();
}
void turn_dos(){ //turn
	motor(l_motor,right);
    motor(r_motor,left);
	msleep(turn_pause_dos);
	ao();
}
void turn_tres(){
	motor(l_motor,right);
    motor(r_motor,left);
	msleep(turn_pause_tres);
	ao();
}
void l_veer(){
    motor(l_motor,v_speed);
}
void r_veer(){
    motor(r_motor,v_speed);
}
void find_line(){
    while (analog(infared) < infared_spot){
    forwards();
    }
    ao();
}
void forwards_dos(){
	motor(l_motor,slow);
    motor(r_motor,slow);
}
void find_wall(){
    while (analog(range_front) >= f_average){
     	forwards_dos();
    if (analog(infared) < infared_spot){
        l_veer();
    }
    if (analog(infared) > infared_spot){
        r_veer();
    }
    ao();
  }
}
void find_wall_dos(){
    while (analog(range_front) >= f_dos){
     	forwards_dos();
    if (analog(infared) < infared_spot){
        l_veer();
    }
    if (analog(infared) > infared_spot){
        r_veer();
    }
    ao();
  }
}

int main()
{
	forwards();
	msleep(pause);
	turn();
	forwards();
	msleep(straight);
	turn_dos();
	find_line();
	find_wall();
	turn_tres();
	find_line();
	find_wall_dos();
    return 0;
}
