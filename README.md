# Play-Baseball
simulation of a baseball game

import java.util.Scanner;

public class LetsPlayBaseball
{
	public static void main(String args[])
	{
		//Declaring and initializing variables
		String team1 = "";
		String team2 = "";
		int hit = 0;
		int score = 0;
		int sumScore1 = 0;
		int sumScore2 = 0;
		int nOut = 0;
		int player1 = 0;
		//player1 is the batter
		int player2 = 0;
		int player3 = 0;
		int player4 = 0;
		//only 4 players because the defense can have a max of four players on the field at once
		//when a player = 0, they are off-field, player = 1, first base, player = 4, returned to home
		int v1 = 0;
		int v2 = 0;
		int v3 = 0;
		int v4 = 0;
		boolean team2Turn = false;
		int t = 0;
		
		Scanner team = new Scanner (System.in);
		
		System.out.println("In baseball, the player at bat can make several different types of hits, including:\n"
				+ "\nsingle" + "\ndouble" + "\ntriple" + "\nrun" + "\nout");
		
		System.out.println("\nEnter the name of Team 1: ");
		team1 = team.nextLine();
		
		System.out.println("\nEnter the name of Team 2: ");
		team2 = team.nextLine();
		
		for (int n = 1; n <= 9; n++) {
			//use of for loop because there is a set number of innings in a baseball game (9)

			System.out.println("\nInning: " + n);
			
			while (nOut < 6) {
			//when both teams have had 3 outs, the inning ends and a new one begins
				if (nOut < 3) {
					System.out.print("\nTeam " + team1);
				} else {
					System.out.print("\nTeam " + team2);
					team2Turn = true;
			
					while (t == 0) {
					t = t + 1;
					//this while loop will only happen once when team2 comes up to bat
					//resetting everything
					score = 0;
					player1 = player2 = player3 = player4 = 0;
					}
				} 
				
				System.out.println();
				
				hit = (int)(Math.random() * 5 + 0);
				//generates numbers between 0 and 4
				
				  player1 = hit;
					
					if (player4 == 0) {
						//there is no player4 on the field, so its position is not affected
						if (player3 == 0) {
							if (player2 > 0) {
								if (player1 >= player2) {
									player2 = player1 + 1;
									//player1 forces player2 to move
								}
							}
						} else {
							if (player1 >= player2) {
								player2 = player1 + 1;
							}
							
							if (player2 >= player3) {
							player3 = player2 + 1;
							}
						}
					} else {
						player2 = player2 + 1;
						player3 = player3 + 1;
						player4 = player4 + 1;
					}
					
					if (hit == 4) {	
						System.out.println("Home run!");
						if (player4 == 0) {
							if (player3 == 0) {
								if (player2 == 0) {
									score = 1;
									//there was only the batter on the field, so only he gets a home run, gaining 1 point
								} else {
									score = 2;
									//scores the home run made by player1 (the batter) as well as the run by player2
								}
							} else {
								score = 3;
							}
						} else {
							score = 4;	
						}
						
						player1 = player2 = player3 = player4 = 0;
						//after a home run, there are no players left on the field
						
					} else if (hit == 1) {
						System.out.println("Single");
						if (player4 >= 4) {
							score = 1;
							//player 4 returns to home
						} else if (player4 == 0) {
							if (player3 >= 4) {
								score = 1;
								player3 = 0;
							} else if (player3 == 0) {
								if (player2 >= 4) {
									score = 1;
									player2 = 0;
								}
							} else {
								score = 0;
							}
						}
	
						//storing the positions of the players
							v3 = player3;
							v2 = player2;
							v1 = player1;
							/*the value of player4 is not stored, because if there were originally 4 players on the field
							*and player1 moved forward, player4 would have advanced to home, gaining a point and exiting the field*/
							
							//the old player 3 becomes player 4 in the new game, etc.
							player4 = v3;
							player3 = v2;
							player2 = v1;
							player1 = 0; 
							 
					} else if (hit == 2) {
						System.out.println("Double");
						if (player4 > 0) {
							score = 2;
							player3 = player4 = 0;
						} else if (player4 == 0) {
							if (player3 >= 4) {
								if (player2 >= 4) {
									score = 2;
									player2 = player3 = 0;
								} else {
									score = 1;
									player3 = 0;
								}
							} else if (player3 == 0) {
								if (player2 >= 4) {
									score = 1;
									player2 = 0;
								} else {
									score = 0;
								}
							}
						}
							
						  v3 = player3;
							v2 = player2;
							v1 = player1;
							
							player4 = v3;
							player3 = v2;
							player2 = v1;
							player1 = 0; 		
						
					} else if (hit == 3) {
						System.out.println("Triple");
						if (player4 > 0) {
							score = 3;
							player2 = player3 = player4 = 0;
						} else if (player4 == 0) {
							if (player3 > 0) {
								score = 2;
								player2 = player3 = 0;
							} else if (player3 == 0) {
								if (player2 > 0) {
									score = 1;
									player2 = 0;
								} else {
									score = 0;
								}
							}
						}
							
						  v3 = player3;
							v2 = player2;
							v1 = player1;
							
							player4 = v3;
							player3 = v2;
							player2 = v1;
							player1 = 0; 	
					
					} else if (hit == 0) {
						System.out.println("Out!");
						score = 0;
						nOut = nOut + 1;
					} else {
						System.out.println("That is not a valid input.");
					}	
				
				if (team2Turn != true) {
					sumScore1 = sumScore1 + score;
					System.out.println("Sum of scores of Team " + team1 + ": " + sumScore1);
				} else {
					sumScore2 = sumScore2 + score;
					System.out.println("Sum of scores of Team " + team2 + ": " + sumScore2);
				}
				
				score = 0;
				//reset the value of the score for the next batter
				}
			
			System.out.println("\nOverall score after inning " + n + ": "
					+ "\nTeam " + team1 + ": " + sumScore1
					+ "\nTeam " + team2 + ": " + sumScore2);
		
			if (n == 9) {
				if (sumScore1 == sumScore2) {
				//if the scores are equal after the 9th inning, the innings loop is continued
					n = 8;
					System.out.println("\nTies are not allowed in baseball");
				} else {
					n = 9;
				}
			}
				
			//resetting everything after the inning is over
			nOut = 0;
			team2Turn = false;
		}
		
		System.out.println("\nThe game is over!");	
		
		System.out.println("\nFinal score: "
					+ "\nTeam " + team1 + ": " + sumScore1
					+ "\nTeam " + team2 + ": " + sumScore2);
		
		if (sumScore1 > sumScore2) {
			System.out.println("\nThe " + team1 + " win!");
		} else {
			System.out.println("\nThe " + team2 + " win!");
		}
	}
}


