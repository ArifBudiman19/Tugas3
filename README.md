Tugas3 Gomoku GUI
======

Repository ini masih belum sempurna dimohon bantuannya untuk menyempurnakannya

======
Codingan kak Remi

import java.awt.BorderLayout;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;

public class TicTacToeMain {
	public static void main(String[] args) {
		TicTacToeGUI gui = new TicTacToeGUI();
		gui.setSize(300, 300);
		gui.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		gui.setVisible(true);
	}
}

class TicTacToeGUI extends JFrame {
	private final int ROWS = 19;
	private final int COLS = 19;
	private boolean turn;
	private JPanel panelAtas;
	private JPanel panelTengah;
	private JPanel panelBawah;
	private JLabel labelJudul;
	private JLabel labelStatus;
	private JButton[][] tombol;

	public TicTacToeGUI() {

		// Bagian Atas
		panelAtas = new JPanel();
		panelAtas.setLayout(new FlowLayout());
		labelJudul = new JLabel("TicTacToeGUI");
		panelAtas.add(labelJudul);
		this.add(panelAtas, BorderLayout.NORTH);

		// Bagian Bawah
		panelBawah = new JPanel();
		labelStatus = new JLabel("Sekarang giliran pemain 1");
		panelBawah.add(labelStatus);
		this.add(panelBawah, BorderLayout.SOUTH);

		// Bagian Tengah
		panelTengah = new JPanel();
		panelTengah.setLayout(new GridLayout(ROWS, COLS));
		tombol = new JButton[ROWS][COLS];
		for (int i = 0; i < ROWS; i++) {
			for (int j = 0; j < COLS; j++) {
				tombol[i][j] = new JButton();
				tombol[i][j].addActionListener(new ButtonListener());
				panelTengah.add(tombol[i][j]);
			}
		}
		this.add(panelTengah, BorderLayout.CENTER);
	}

	class ButtonListener implements ActionListener {

		@Override
		public void actionPerformed(ActionEvent e) {
			// TODO Auto-generated method stub
			JButton diPencet = (JButton) e.getSource();
			if (!turn) {
				diPencet.setText("O");
				labelStatus.setText("Giliran pemain 2");
			} else {
				diPencet.setText("X");
				labelStatus.setText("Giliran pemain 1");
			}
			diPencet.setEnabled(false);
			turn = !turn;
		}

	}
}

=========
kodingan coba sendiri

==============================================================
/**
 * Kelas ini dibuat untuk mempresentasikan sebuah papan permain gomoku
 * yang memiliki ukuran 19 x 19
 * 
 * @author Arif Budiman
 * @version 1.0
 *
 */
public class Board 
{
	private char[][] papan;
	private int sizePapan;
	
	// TODO: Membuat consturctor Papan
	/**
	 * constructor ini dibuat dengan mengisi seluruh slot pada papan
	 * dengan titik
	 * 
	 * @param sizePapan adalah ukuran papan yaitu 19 x 19
	 * 
	 */
	public Board(int sizePapan)
	{
		this.sizePapan = sizePapan;
		this.papan = new char[sizePapan][sizePapan];
		for(int row = 0; row < papan.length; row++){
			for(int col = 0; col < papan[row].length; col++)
			{
				papan[row][col] = '.';
			}
		}
	}

	/**
	 * Method yang mengembaikan Array Papan
	 * @return Array of Char
	 */
	public char[][] getPapan()
	{
		return papan;
	}
	
	/**
	 * Method yang mengembalikan nilai ukuran papan
	 * @return int ukuran papan
	 */
	public int getSizePapan()
	{
		return sizePapan;
	}

	/**
	 * Method ini dibuat untuk mengubah ukuran papan
	 * @param sizePapan
	 */
	public void setSizePapan(int sizePapan)
	{
		this.sizePapan = sizePapan;
	}
	
	/**
	 * Method ini mengembalikan nilai papan pada slot tertentu
	 * @param x adalah koordinat pada x
	 * @param y adalah koordinat pada y
	 * @return nilai papan slot tertentu
	 */
	public int getPapanValue(int row, int col)
	{
		return papan[row][col];
	}
	
	/**
	 * Method ini merubah nilai papan menjadi piece tertentu pada slot tertentu
	 * @param x adalah koordinat x tempat piece akan dimasukan
	 * @param y adalah koordinat y tempat piece akan dimasukan
	 * @param piece adalah kepingan hitam atau putih pada permainan gomoku
	 */
	public void setPiece(int row, int col, char piece)
	{
		papan[row][col] = piece;
	}
}

=========================================================================

/**
 * Kelas ini dibuat untuk mengidentifikasi pemain dan membuat pemain.
 * @author Arif Budiman
 * @version 1.1
 *
 */
public class Player
{
	private char peace;
	private String nama;
	
	/**
	 * Constructor ini berisi nama pemain dan symbol kepingan 
	 * @param peace 
	 * @param nama
	 */
	public Player(char peace, String nama)
	{
		this.peace = peace;
		this.nama = nama;
	}
	
	/**
	 * Method untuk mengambil char Kepingan
	 * @return char Kepingan
	 */
	public char getPeace() 
	{
		return peace;
	}
	
	/**
	 * Method untuk mengganti kepingan
	 * @param peace (kepingan)
	 */
	public void setPeace(char peace)
	{
		this.peace = peace;
	}
	
	/**
	 * Method yang mengembalikan Nama Player
	 * @return String namaPlayer
	 */
	public String getNama() 
	{
		return nama;
	}
	
	/**
	 * Method yang digunakan untuk merubah nama Player
	 * @param nama
	 */
	public void setNama(String nama)
	{
		this.nama = nama;
	}
}

===========================================================================

import java.awt.BorderLayout;
import java.awt.Color;
import java.awt.FlowLayout;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JPanel;

public class GomokuGame  {
	public static void main(String[] args) {
		GameGUI gui = new GameGUI();
		gui.setSize(850, 700);
		gui.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		gui.setVisible(true);
	}
}

class GameGUI extends JFrame{
	/**
	 * 1.1
	 */
	private static final long serialVersionUID = 1L;
	private final int ROWS = 19;
	private final int COLS = 19;
	private boolean turning;
	private JPanel panelAtas;
	private JPanel panelTengah;
	private JPanel panelBawah;
	private JLabel labelJudul;
	private JLabel labelStatus;
	private JButton[][] tombol;
	public int x;
	public int y;
	public static int maxSet = 19*19;
	Board papan;
	final int SIZE_PAPAN = 19;
	String win;
	int turn;
	Player player1;
	Player player2;
	
	public GameGUI(){
		
		// Bagian Atas
		panelAtas = new JPanel();
		panelAtas.setLayout(new FlowLayout());
		labelJudul = new JLabel("GOMOKU GUI");
		panelAtas.add(labelJudul);
		this.add(panelAtas, BorderLayout.NORTH);
		
		// Bagian Bawah
		panelBawah = new JPanel();
		labelStatus = new JLabel("Sekarang giliran pemain 1");
		panelBawah.add(labelStatus);
		this.add(panelBawah, BorderLayout.SOUTH);
		
		// Bagian Tengah
		panelTengah = new JPanel();
		panelTengah.setLayout(new GridLayout(ROWS, COLS));
		tombol = new JButton[ROWS][COLS];
		for(int i = 0; i < ROWS; i++){
			for(int j = 0; j < COLS; j++){
				tombol[i][j] = new JButton();
				tombol[i][j].setName(i+","+j);
				if((i+j)%2 == 0){
					tombol[i][j].setBackground(Color.LIGHT_GRAY);
				}else{
					tombol[i][j].setBackground(Color.cyan);
				}
				tombol[i][j].addActionListener(new ButtonListener());
				panelTengah.add(tombol[i][j]);
			}
		}
		this.add(panelTengah, BorderLayout.CENTER);
		
		player1 = new Player('B', "hitam");
		player2 = new Player('W', "putih");
		papan = new Board(SIZE_PAPAN);
		win = "";
		turn = 0;
	
	}

	class ButtonListener implements ActionListener{
		

		@Override
		public void actionPerformed(ActionEvent e) {
			// TODO Auto-generated method stub
			JButton diPencet = (JButton) e.getSource();
			System.out.println(diPencet.getName());
			String pieceName = player1.getNama();
			char piece = player1.getPeace();
			turn++;
			// jika giliran angka genap maka pieceName dan piece diubah menjadi Player2
			if (turn % 2 == 0)
			{
				pieceName = player2.getNama();
				piece = player2.getPeace();
			}
			String[] cordinates = diPencet.getName().split(",");
			int x = Integer.parseInt(cordinates[0]);
			int y = Integer.parseInt(cordinates[1]);
			papan.setPiece(x, y, piece);
			maxSet--;
				if(!turning){
					diPencet.setText("O");
					labelStatus.setText("Giliran pemain 2");
				}else{
					diPencet.setText("X");
					labelStatus.setText("Giliran pemain 1");
				}
				diPencet.setEnabled(false);
				turning = !turning;
				if (cek(x,y))
				{
					JOptionPane.showMessageDialog(diPencet,"Selamat! " + pieceName + " menang dalam " + turn + " langkah");
					System.exit(0);
				}
			
				// mengecek permainan seri
				if(maxSet == 0)
				{
					JOptionPane.showMessageDialog(diPencet, "Permainan Seri");
					System.exit(0);
				}
			}
		}
		
		public boolean cek(int row, int col) 
		{
			/*
			 * membuat arah dengan array dCol dan dRow 
			 * dengan 8 arah (beruruntan) 
			 * horizontal kekiri
			 * horizontal kekanan
			 * vertikal keatas
			 * vertikal kebawah
			 * diagonal \ kebawah
			 * diagonal \ keatas
			 * diagonal / kebawah
			 * diagonal / keatas
			 */
			int[] dCol = { 0,0,-1,1,-1,1, 1,-1};
			int[] dRow = {-1,1, 0,0,-1,1,-1, 1};
			/*
			 * looping 4 x dan menggabungkan arah arah yang berlawanan 
			 */
			for(int arah = 0; arah < 4; arah++)
			{
				/*
				 * deklarasi kepada dan buntut sebagai acuan
				 */
				int headX = row;
				int headY = col;
				int tailX = row;
				int tailY = col;
				// memakai arah dRow dan dCol index genap
				while ( (headX + dRow[arah*2] >= 0) && (headY + dCol[arah*2] >= 0) 
						&& (headX + dRow[arah*2] < 19) && (headY + dCol[arah*2] < 19)
						&& (papan.getPapanValue(headX + dRow[arah*2], headY + dCol[arah*2]) == papan.getPapanValue(row,col)))
				{
					headX += dRow[arah*2];
					headY += dCol[arah*2];
				}
				// memakai arah dRow dan dCol index ganjil
				while ( (tailX+dRow[arah*2+1] >= 0) && (tailY+dCol[arah*2+1] >= 0) 
						&& (tailX+dRow[arah*2+1] < 19) && (tailY+dCol[arah*2+1] < 19) 
						&& (papan.getPapanValue(tailX + dRow[arah*2+1], tailY + dCol[arah*2+1]) == papan.getPapanValue(row,col)))
				{ 
					tailX += dRow[arah*2+1];
					tailY += dCol[arah*2+1];
				}
				/*
				 * mencari nilai maximum dari selisih head dan tail x y 
				 */
				int banyakCharacter = Math.max(Math.abs(headY-tailY)+1 , Math.abs(headX-tailX)+1);
				if(banyakCharacter >= 5)
				{ 
					return true;
				}
			}
			return false;
		}
}
