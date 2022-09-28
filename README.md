# androidmosquemaplocator
surabaya mosque map locator (android app)

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */

package peta;

import java.awt.Color;
import java.awt.Graphics;
import java.awt.Graphics2D;
import java.awt.geom.Ellipse2D;
import java.awt.geom.Line2D;
import java.util.LinkedList;
import javax.swing.JOptionPane;

/**
 *
 * @author Toshiba
 */

public class ViewPeta extends javax.swing.JFrame {
 LinkedList<Titik> kumpulanTitik = new LinkedList<Titik>();
 LinkedList<Garis> kumpulanGaris = new LinkedList<Garis>();
 double MAP_WIDTH=1280;
 double MAP_HEIGHT=800;
 double xhome, yhome;
 double xgeser=0,ygeser=0;
 double skala=1300;
 double xmargin=800, ymargin=300;
 Graphics2D G2;
 int icari = -1;
   
    /**
     * Creates new form ViewPeta
     * int x =  (int) ((MAP_WIDTH/360.0) * (180 + lon));
       int y =  (int) ((MAP_HEIGHT/180.0) * (90 - lat));
     */
    public ViewPeta() {
        initComponents();
        isidatalokasi();
        tentukanhome();
        isidatajalan();
    }

    public void paint (Graphics g) {
    Graphics2D g2 = (Graphics2D) g;
    Titik a; 
    double x,y;
    double xv, yv;
    G2 = (Graphics2D) g;
    g2.setColor(Color.white);
    //g2.drawRect(0, 0, getWidth(), getHeight());
    g2.fillRect(0, 0, getWidth(), getHeight());
    g2.setColor(Color.black);
        for (int i = 0; i < kumpulanTitik.size(); i++) {
            a= kumpulanTitik.get(i);
            //System.out.println(a.getLat()+"  "+ a.getLon()+"  "+ a.getLokasi());
          //  x= getx(a.getLon());
           // y= gety(a.getLat());
            //xv= (x-xhome)*skala+xmargin;
       
            // yv= (y-yhome)*skala+ymargin;
            xv = konversikeXlayar(a.getLon());
            yv = konversikeYlayar(a.getLat());
            //System.out.println(xv+"  "+yv+"  "+ a.getLokasi());
            // draw Ellipse2D.Double
g2.draw(new Ellipse2D.Double(xv, yv,
                             5,
                             5));
//g2.drawString(a.getLokasi(), xv, yv);
g2.drawString(a.getLokasi(), (int) xv, (int) yv);


            
        }
        Garis b;
        Titik awal,akhir; 
        double x1,y1,x2,y2;
        for (int i = 0; i < kumpulanGaris.size(); i++) {
          b= kumpulanGaris.get(i);
          awal= kumpulanTitik.get(b.getAwal());
          akhir=kumpulanTitik.get(b.getAkhir());
         
          x1= konversikeXlayar(awal.getLon());
          y1= konversikeYlayar(awal.getLat());
          x2= konversikeXlayar(akhir.getLon());
          y2= konversikeYlayar(akhir.getLat());
          
// draw Line2D.Double
g2.draw(new Line2D.Double(x1, y1, x2, y2));
Double jarak = hitungJarak (awal.getLon(),awal.getLat(),akhir.getLon(),akhir.getLat());
          g2.drawString(jarak.toString(), (int) (x1+x2)/2, (int) (y1+y2)/2);
            
        }
        Titik c;
       // double x, y;
        if (icari>=0) {
          c = kumpulanTitik.get(icari);
          x = konversikeXlayar(c.getLon());
          y = konversikeYlayar(c.getLat());
          g2.draw(new Ellipse2D.Double(x, y,
                             10,
                             10));
            System.out.println("ketemu");
        }
}
    
    /**
     * This method is called from within the constructor to initialize the form.
     * WARNING: Do NOT modify this code. The content of this method is always
     * regenerated by the Form Editor.
     */
    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jButton1 = new javax.swing.JButton();
        jButton2 = new javax.swing.JButton();
        jButton3 = new javax.swing.JButton();
        jButton4 = new javax.swing.JButton();
        button1 = new java.awt.Button();
        button2 = new java.awt.Button();
        button3 = new java.awt.Button();
        button4 = new java.awt.Button();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);

        jButton1.setText("CLOSE");
        jButton1.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jButton1ActionPerformed(evt);
            }
        });

        jButton2.setText("Cari");
        jButton2.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jButton2ActionPerformed(evt);
            }
        });

        jButton3.setText("zoom in");
        jButton3.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jButton3ActionPerformed(evt);
            }
        });

        jButton4.setText("zoom out");
        jButton4.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                jButton4ActionPerformed(evt);
            }
        });

        button1.setLabel("atas");
        button1.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                button1ActionPerformed(evt);
            }
        });

        button2.setLabel("kanan");
        button2.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                button2ActionPerformed(evt);
            }
        });

        button3.setLabel("kiri");
        button3.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                button3ActionPerformed(evt);
            }
        });

        button4.setLabel("bawah");
        button4.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                button4ActionPerformed(evt);
            }
        });

        javax.swing.GroupLayout layout = new javax.swing.GroupLayout(getContentPane());
        getContentPane().setLayout(layout);
        layout.setHorizontalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(layout.createSequentialGroup()
                .addGap(28, 28, 28)
                .addComponent(jButton1)
                .addGap(38, 38, 38)
                .addComponent(jButton2)
                .addGap(31, 31, 31)
                .addComponent(jButton3)
                .addGap(38, 38, 38)
                .addComponent(jButton4)
                .addContainerGap(883, Short.MAX_VALUE))
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                .addGap(0, 0, Short.MAX_VALUE)
                .addComponent(button3, javax.swing.GroupLayout.PREFERRED_SIZE, 41, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(40, 40, 40)
                .addComponent(button2, javax.swing.GroupLayout.PREFERRED_SIZE, 40, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addContainerGap())
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                .addContainerGap(javax.swing.GroupLayout.DEFAULT_SIZE, Short.MAX_VALUE)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
                    .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                        .addComponent(button4, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(44, 44, 44))
                    .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                        .addComponent(button1, javax.swing.GroupLayout.PREFERRED_SIZE, 52, javax.swing.GroupLayout.PREFERRED_SIZE)
                        .addGap(45, 45, 45))))
        );
        layout.setVerticalGroup(
            layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGroup(javax.swing.GroupLayout.Alignment.TRAILING, layout.createSequentialGroup()
                .addContainerGap(612, Short.MAX_VALUE)
                .addComponent(button1, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.TRAILING)
                    .addComponent(button2, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                    .addComponent(button3, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE))
                .addPreferredGap(javax.swing.LayoutStyle.ComponentPlacement.RELATED)
                .addComponent(button4, javax.swing.GroupLayout.PREFERRED_SIZE, javax.swing.GroupLayout.DEFAULT_SIZE, javax.swing.GroupLayout.PREFERRED_SIZE)
                .addGap(49, 49, 49)
                .addGroup(layout.createParallelGroup(javax.swing.GroupLayout.Alignment.BASELINE)
                    .addComponent(jButton1)
                    .addComponent(jButton2)
                    .addComponent(jButton3)
                    .addComponent(jButton4))
                .addGap(24, 24, 24))
        );

        pack();
    }// </editor-fold>                        

    private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
    this.dispose();
    }                                        

    private void jButton2ActionPerformed(java.awt.event.ActionEvent evt) {                                         
        String dicari =  JOptionPane.showInputDialog("masukkan input"); 
        icari = cariLokasi(dicari);
        repaint();
    }                                        

    private void jButton3ActionPerformed(java.awt.event.ActionEvent evt) {                                         
     skala *= 1.2 ;
     repaint();
    }                                        

    private void jButton4ActionPerformed(java.awt.event.ActionEvent evt) {                                         
       
        skala*= 0.8;
        repaint();
    }                                        

    private void button2ActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here: kanan
        xgeser-=10;
        repaint();
              
    }                                       

    private void button3ActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here: kiri
        xgeser+=10;
        repaint();
    }                                       

    private void button1ActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here: atas
         ygeser+=10;
         repaint();
       
    }                                       

    private void button4ActionPerformed(java.awt.event.ActionEvent evt) {                                        
        // TODO add your handling code here: bawah
        ygeser-=10;
         repaint();
    }                                       

    /**
     * @param args the command line arguments
     */
    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(ViewPeta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(ViewPeta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(ViewPeta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(ViewPeta.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        /* Create and display the form */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new ViewPeta().setVisible(true);
            }
        });
    }

    // Variables declaration - do not modify                     
    private java.awt.Button button1;
    private java.awt.Button button2;
    private java.awt.Button button3;
    private java.awt.Button button4;
    private javax.swing.JButton jButton1;
    private javax.swing.JButton jButton2;
    private javax.swing.JButton jButton3;
    private javax.swing.JButton jButton4;
    // End of variables declaration                   

    private void isidatalokasi() {
       kumpulanTitik.add(new Titik(-7.282320, 112.793010 , "MASJID MANARUL ILMI" ) );
       kumpulanTitik.add(new Titik(-7.313873, 112.734303 , "MASJID BAITUL HAQ"));
       kumpulanTitik.add(new Titik(-7.336587, 112.715237 , "MASJID AL AKBAR"));
       kumpulanTitik.add(new Titik(-7.258213, 112.748370 , "MASJID AL MUHAJIRIN"));
       kumpulanTitik.add(new Titik(-7.252099, 112.746975 , "MASJID CHENG-HO"));
       kumpulanTitik.add(new Titik(-7.294919, 112.739598 , "MASJID AL FALAH" ));
       kumpulanTitik.add(new Titik(-7.229516, 112.742842 , "MASJID AGUNG SUNAN AMPEL" ));
       kumpulanTitik.add(new Titik(-7.214047, 112.733003 , "MASJID MUJAHIDIN" ));
       kumpulanTitik.add(new Titik(-7.332348, 112.757165 , "MASJID BAITURROZAQ SIER SURABAYA" ));
       kumpulanTitik.add(new Titik(-7.293090, 112.655012 , "GEREJA KATOLIK SANTO YAKOBUS" ));
       kumpulanTitik.add(new Titik(-7.249848, 112.646047 , "GEREJA PANTEKOSTA PUSAT SURABAYA"));
       kumpulanTitik.add(new Titik(-7.267675, 112.692010 , "GEREJA KATOLIK ST ALOYSIUS GONZAGA"));
       kumpulanTitik.add(new Titik(-7.270007, 112.738552 , "GEREJA MAWAR SHARON"));
       kumpulanTitik.add(new Titik(-7.256079, 112.754317 , "GEREJA KRISTUS RAJA"));
       kumpulanTitik.add(new Titik(-7.242211, 112.736598 , "GEREJA KATOLIK KELAHIRAN SANTA PERAWAN MARIA" ));
       kumpulanTitik.add(new Titik(-7.247401, 112.790499 , "GEREJA KATOLIK ST MARINUS YOHANES" ));
       kumpulanTitik.add(new Titik(-7.252868, 112.755032 , "PURA TIRTA WENING" ));
       kumpulanTitik.add(new Titik(-7.277527, 112.702807 , "PURA SONO PARE GIRI" ));
       kumpulanTitik.add(new Titik(-7.279503, 112.758923 , "PURA TIRTA GANGGA" ));
       kumpulanTitik.add(new Titik(-7.231433, 112.721702 , "PURA AGUNG JAGAT KARANA SURABAYA" ));
       kumpulanTitik.add(new Titik(-7.270758, 112.700222 , "WIHARA BUDHA MATRIA" ));
       kumpulanTitik.add(new Titik(-7.288440, 112.740352 , "WIHARA VIMALAKIRTI" ));
       kumpulanTitik.add(new Titik(-7.247091, 112.740236 , "WIHARA MAHAVIRA GRAHA" ));
       kumpulanTitik.add(new Titik(-7.247944, 112.745779 , "KLENTENG PAK KIK BIO" ));
       kumpulanTitik.add(new Titik(-7.247197, 112.802318 , "KLENTENG SANGGAR AGUNG" ));
       kumpulanTitik.add(new Titik(-7.235981, 112.742914 , "KLENTENG HONG TIEK HIAN" ));
    }

    private double getx(double lon) {
       double x =  ((MAP_WIDTH/360.0) * (180 + lon));
     return x;
    }

    private double gety(double lat) {
        double y =  ((MAP_HEIGHT/180.0) * (90 - lat));
     return y;
    }

    private void tentukanhome() {
        Titik a; 
    a= kumpulanTitik.get(0);
            //System.out.println(a.getLat()+"  "+ a.getLon()+"  "+ a.getLokasi());
            xhome= getx(a.getLon());
            yhome= gety(a.getLat());
    }


    private void isidatajalan() {
       /*kumpulanGaris.add(new Garis(0,1," " ));
       kumpulanGaris.add(new Garis(0,5,"  " ));
       kumpulanGaris.add(new Garis(0,8,"  " ));
       kumpulanGaris.add(new Garis(1,4,"  " ));
       kumpulanGaris.add(new Garis(1,20,"  " ));
       kumpulanGaris.add(new Garis(2,18,"  " ));
       kumpulanGaris.add(new Garis(2,19,"  " ));
       kumpulanGaris.add(new Garis(3,5,"  " ));
       kumpulanGaris.add(new Garis(3,8," " ));
       kumpulanGaris.add(new Garis(3,15,"  " ));
       kumpulanGaris.add(new Garis(3,18,"  " ));
       kumpulanGaris.add(new Garis(4,6,"  " ));
       kumpulanGaris.add(new Garis(4,8,"  " ));
       kumpulanGaris.add(new Garis(5,17,"  " ));
       kumpulanGaris.add(new Garis(5,20,"  " ));
       kumpulanGaris.add(new Garis(6,7,"  " ));
       kumpulanGaris.add(new Garis(6,18,"  " ));
       kumpulanGaris.add(new Garis(7,11," " ));
       kumpulanGaris.add(new Garis(7,18,"  " ));
       kumpulanGaris.add(new Garis(9,13,"  " ));
       kumpulanGaris.add(new Garis(9,14,"  " ));
       kumpulanGaris.add(new Garis(9,15,"  " ));
       kumpulanGaris.add(new Garis(9,16,"  " ));
       kumpulanGaris.add(new Garis(10,11,"  " ));
       kumpulanGaris.add(new Garis(10,12,"  " ));
       kumpulanGaris.add(new Garis(10,20,"  " ));
       kumpulanGaris.add(new Garis(12,17," " ));
       kumpulanGaris.add(new Garis(12,21,"  " ));
       kumpulanGaris.add(new Garis(13,15,"  " ));
       kumpulanGaris.add(new Garis(13,16,"  " ));
       kumpulanGaris.add(new Garis(13,17,"  " ));
       kumpulanGaris.add(new Garis(14,17,"  " ));
       kumpulanGaris.add(new Garis(14,21,"  " ));
       kumpulanGaris.add(new Garis(15,19,"  " ));
       kumpulanGaris.add(new Garis(16,19," " ));
       kumpulanGaris.add(new Garis(17,21,"  " ));*/
    }

    private double konversikeXlayar(double lon) {
     double x=  getx(lon);
            
        double xv= (x-xhome)*skala+xmargin+xgeser;
        return xv;
               
    }

    private double konversikeYlayar(double lat) {
      double y = gety(lat);
      
      double yv = (y-yhome)*skala+ymargin+ygeser;
      return yv;
      
    }

    private int cariLokasi(String dicari) {
        int hasil = -1;
        Titik b;
        for (int i = 0; i < kumpulanTitik.size(); i++) {
            b = kumpulanTitik.get(i);
            if(dicari.equalsIgnoreCase(b.getLokasi())) {
                hasil = i;
                break;
            }
        }
     return hasil;
    }

    private double hitungJarak(double lon1, double lat1, double lon2, double lat2) {
       final int R = 6371; // Radious of the earth
        Double latDistance = toRad(lat2-lat1);
        Double lonDistance = toRad(lon2-lon1);
        Double a = Math.sin(latDistance / 2) * Math.sin(latDistance / 2) +
                   Math.cos(toRad(lat1)) * Math.cos(toRad(lat2)) *
                   Math.sin(lonDistance / 2) * Math.sin(lonDistance / 2);
        Double c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));
        Double distance = R * c;
        return distance ;
    }

    private Double toRad(double value) {
        return value * Math.PI / 180;
    }
}
