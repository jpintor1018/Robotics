# Robotics

import lejos.nxt.*;

import lejos.nxt.ColorSensor.Color;

import lejos.*;

public class HelloWorld

{

    public static void main(String[] args)
    
    {
        System.out.println("Lego Robotic");

        UltrasonicSensor sonar = new UltrasonicSensor(SensorPort.S1);
        ColorSensor cs= new ColorSensor(SensorPort.S2, ColorSensor.TYPE_COLORFULL); 
        cs.setFloodlight(true);


        Motor.C.forward();
       
        Motor.B.forward();
       

       int dista= sonar.getDistance();
       boolean bak = false;

       while (dista >= 20 && bak==false)
      {
              dista= sonar.getDistance();

               if(dista >20 && bak==false)
               {
            	   Motor.C.forward();
            	   Motor.B.forward();
            	  
                   
                   int color = cs.getColorID();

                   if (color == Color.WHITE)
                   {      
                          Sound.twoBeeps();
                          Motor.C.stop();
                          Motor.B.stop();
                          Sound.twoBeeps();
                   }
                   if (color == Color.RED)
                   {
                	   Motor.C.stop();
                	   Motor.B.stop();
                   }
                   
              }
             if( dista <= 25)
             {
                 bak=true;
                
                 Motor.B.rotate(360);
                 Motor.B.rotate(360);
                 Motor.B.rotate(360);
                 Motor.B.rotate(360);
                 
                 int color = cs.getColorID();

                 if (color == Color.GREEN)
                 {      
                         Sound.twoBeeps();
                         Sound.twoBeeps();
                }

                dista= sonar.getDistance();

                Motor.B.rotate(50);
                Motor.B.rotate(-50,true);
                
             }
        

            dista= sonar.getDistance();
           if (dista >20)
               bak=false;
         }
     }

}

