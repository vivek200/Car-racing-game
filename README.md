import java.awt.*;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.applet.*;

import javax.swing.JOptionPane;
public class cargame extends Applet implements Runnable,KeyListener{
   Thread t;
	Image ic,id,ie,ig,ik,il;
	String st="Score : ";int sc;
	String sa="press 's' to start game";
	int a=200,b=-300,cr=435,sp=0,ob=100,oba=-300,obb=-500;

	 String show="     ";
	 Font f;
	public void init()
	 {   
		 f=new Font("Arial",Font.BOLD,20);
		 setFont(f);
		t=new Thread(this);  
		ic=getImage(getCodeBase(),"strip.jpg");
		 id=getImage(getCodeBase(),"line.png");
		 ie=getImage(getCodeBase(),"yellcar.png");
		 ig=getImage(getCodeBase(),"green.png");
		 ik=getImage(getCodeBase(),"blue.png");
		 il=getImage(getCodeBase(),"carc.png");
		 
		 addKeyListener(this);
	 }
	 
	 public void paint(Graphics g)
	 {   
		 
		 g.drawImage(id,380,0,20,1000,this);
	     g.drawImage(id,720,0,20,1000,this);
	     g.drawString(sa, 5, 70);
	     // moving lines
		 g.drawImage(ic,400,b,20,1000,this);
		 g.drawImage(ic,500,b,20,1000,this);
		 g.drawImage(ic,600,b,20,1000,this);
		 g.drawImage(ic,700,b,20,1000,this);
		  // moving obstacle
		 
		 
		 {g.drawImage(ik,435,ob,50,100,this);
		 g.drawImage(ig,535,oba,50,100,this);
		 g.drawImage(il,610,obb,100,100,this);
		 
		 g.drawImage(ie,cr,500,50,100,this);    // 435
		 
		 g.drawString("Score : "+sc, 50, 200);
		 if(sc>=2000)
			 g.setColor(Color.green);
		 if(sc>=4000)
			 g.setColor(Color.YELLOW);
		 if(sc>=6000)
			 g.setColor(Color.RED);
		 if(sc>=8000)
			 g.setColor(Color.BLUE);
		 g.drawString(show,800, 300);
		 }
		 
	 }
	   public void run()
	   {    try{
		          while(true)
		          { 
		        	  if(sc>=2000)
		        		  show="Your score is above 2000";
		        	  
		        	  if(sc>=4000)
		        		  show="Your score is above 4000";
		        		  if(sc>=6000)
		        			  show="Your score is above 6000";
		        		  if(sc>=8000)
		        			  show="Your score is above 8000";
		        	  
		        	  sc=sc+sp+1;
		        	  b=b+3+sp;
		          Thread.sleep(60);
		          if(b>=-3)
		        	b=-342;  
		          ob=ob-4+sp;
		          if(ob>=650)
		        	  ob=-200;
		          
		          oba=oba+6+sp;
		          if(oba>=650)
		        	  oba=-300;

		          obb=obb+15+sp;
		          if(obb>=650)
		        	obb=-100;
		          ob=ob-2;  // this line is written so that car obstacle touches yellocar exactly;
		          repaint();
		          if(ob>=405 && ob<=570 && cr==435)
		          { 
		        	  AudioClip gong=getAudioClip(getDocumentBase(), "Explosion.wav");
		        	  gong.play();
		          JOptionPane.showMessageDialog(this, "game over, your score is :"+sc);
		          
					

		          a=200;b=-300;cr=435;sp=0;ob=100;oba=-300;obb=-500;	  sc=0; 
		          }
		          
		          if(oba>=405 && oba<=570 && cr==535)
		          { 
		        	  AudioClip gong=getAudioClip(getDocumentBase(), "Explosion.wav");
		        	  gong.play();
		          JOptionPane.showMessageDialog(this, "game over, your score is :"+sc);
		          a=200;b=-300;cr=435;sp=0;ob=100;oba=-300;obb=-500; sc=0;
		          }
		          if(obb>=405 && obb<=570 && cr==635)
		          {    
		        	  AudioClip gong=getAudioClip(getDocumentBase(), "Explosion.wav");
		        	  gong.play();
		         
		        	  JOptionPane.showMessageDialog(this, "game over, your score is :"+sc);
		        
		          a=200;b=-300;cr=435;sp=0;ob=100;oba=-300;obb=-500; sc=0;
		          }
		 		
		          
		          
		          }
		   }catch(Exception e){}
		   
		   
		   
	   }

	@Override
	public void keyPressed(KeyEvent kp) {
		
		 if(kp.getKeyCode()==kp.VK_RIGHT)
		 {
			 if(cr==535)
				 cr=635;
			 if(cr==435)
				  cr=535;
			
			 }
		 if(kp.getKeyCode()==kp.VK_LEFT)
		 {
			 if(cr==535)
				 cr=435;
			 if(cr==635)
				 cr=535;
			
			 }		  
		 
		 if(kp.getKeyCode()==kp.VK_UP)
		 {  
		   sp=30;
			 }
		 if(kp.getKeyCode()==kp.VK_DOWN)
		 {  
		   sp=0;
			 }
		 
		 if(kp.getKeyChar()=='s')
		 {   sa="";
			 t.start();  }
	
		
	}

	@Override
	public void keyReleased(KeyEvent arg0) {
		// TODO Auto-generated method stub
		
	}

	@Override
	public void keyTyped(KeyEvent arg0) {
		// TODO Auto-generated method stub
		
	}
	 
}
