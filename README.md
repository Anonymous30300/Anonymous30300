import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

pf=pd.read_csv('Premier League Player data.csv')



def highest():
    print()
    print("-"*65)
    print('Player with highest goal:')
    print("-"*65)
    p=pf.sort_values(by='Goals',ascending=False).head(1)
    print(p[['PLAYER','TEAM','Goals']].to_string(index=None))
    
    print()
    print("-"*65)
    print('Players with least goal')
    print("-"*65)
    p=pf.sort_values(by='Goals',ascending=False).tail(1)
    print(p[['PLAYER','TEAM','Goals']].to_string(index=None))
    print()

def delplayer():
    df=pd.read_csv('Premier League Player data.csv')
    pl=input("Enter player name:")
    for RI,record in df.iterrows():
        if pl==record['PLAYER']:
            df.drop(RI,axis=0,inplace=True)
            df.to_csv('Premier League Player data.csv',index=None)
            print("\nDeleted ",pl," successfully\n")
            break
    else:
        print('\nPlayer not Found')

def Playerinteam():
    print()
    T=np.array(pf.TEAM)
    od=input('CHOOSE TEAM FROM THE FOLLOWING ==> \n\n'+str(np.unique(T))+"\n\n\t : ")
    print("-"*65)
    print(pf.loc[pf.TEAM==od,['Rank','PLAYER','Game_played','Goals','Position']])
    print("-"*65)
   
def leastmatch():
    print()
    print("-"*65)
    print('Player with least matches:')
    print("-"*65)
    p=pf.sort_values(by='Game_played',ascending=False).tail(1)
    print(p[['PLAYER','TEAM','Game_played']].to_string(index=None))
    print("-"*65)
        
def ageplayer():
    print("-"*65)
    pl=pf.sort_values(by='Age',ascending=False)
    print(pl[['PLAYER','TEAM','Age','Game_played']].to_string(index=None))
    print("-"*65)

def positionplay():
    print()
    T=np.array(pf.Position)
    spa=input('CHOOSE POSITION FROM THE FOLLOWING ==> \n\n'+str(np.unique(T))+"\n\n\t : ")
    print(pf.loc[pf.Position==spa,['Rank','TEAM','PLAYER','Game_played','Goals']].to_string(index=None))


def updateplayer():
    df=pd.read_csv('Premier League Player data.csv')
    P=input('Enter Player Name:')
    CI=input('Enter the column to be changed:')
    Data=input('Enter new data:')
    for RI,record in df.iterrows():
        if P == record['PLAYER']:
            if CI in df.columns:
                df.at[df.PLAYER==P,CI]=Data
                print("    Changed Data   ")
                print("___________________")
                print(df.loc[df.PLAYER==P,['PLAYER',CI]])
                df.to_csv('Premier League Player data.csv',index=None)
                break
            else:
                print("Column Label incorrect")
                break
    else:
        print('Data incorrect.')
         
def DataAnalysis():
    while True:
        print("-"*65)
        print("|                                                \t\t|")
        print('|\t\t<<<<<<<ＤＡＴＡ ＡＮＡＬＹＳＩＳ>>>>>>>         \t|')
        print("|                                                \t\t|")
        print('|\t1.PLAYER WITH HIGHEST GOAL/LEAST GOAL           \t|')
        print('|\t2.PLAYER WITH LEAST MATCHES AND SCORED HIGHEST GOAL\t|')
        print('|\t3.SHOW PLAYERS IN A TEAM                            \t|')
        print('|\t4.SHOW PLAYERS IN SAME POSITION                     \t|')
        print('|\t5.SORT PLAYERS BASED ON AGE                         \t|')
        print('|\t6.UPDATE SCORE DETAILS OF THE PLAYER                \t|')
        print('|\t7.DELETE A PLAYER                                   \t|')
        print('|\t8.SHOW STATUS                                       \t|')
        print('|\t9.EXIT                                              \t|')
        print("|                                                \t\t|")
        print("-"*65)
        mn=int(input('Choose option from above:'))
        if mn == 1:
            highest()
        elif mn ==2:
            leastmatch()
        elif mn == 3:
            Playerinteam()
        elif mn==4:
            positionplay()
        elif mn == 5:
            ageplayer()
        elif mn==6:
            updateplayer()
        elif mn==7:
            delplayer()
        elif mn ==8:
            print(pf)
        elif mn ==9:
            break
        else:
            print("Invalid option.Choose option 1 - 9")


def BarPlayer():
    Names=[]
    for x in pf.PLAYER:
        F_L=x.partition(' ')
        if F_L[2] == '':
            Names.append(F_L[0])
        else:
            Names.append(F_L[2])
    pf.plot(x='PLAYER',y='Game_played',kind='barh',color='silver',edgecolor='darkblue')
    plt.title('NUMBER OF GAMES PLAYED BY EACH PLAYER',color='orange')
    plt.yticks(np.arange(len(Names)),Names)
    plt.ylabel("<       NUMBER OF GAMES PLAYED           >")
    plt.show()    



def HistPlayer():
   F=np.arange(1000,3500,200)
   plt.hist(pf['Minutes_played'],bins=F,color='red',edgecolor='k')
   plt.xlabel('Ranges of Minutes_played')
   plt.ylabel('<------------No. of Players----------------->')
   plt.title('Players Vs Minutes Played')
   plt.show() 



def ScatterPlot():
    plt.scatter(pf['Goals'],pf['Minutes_played'],color='red',marker='^')
    plt.xlabel('Goals',fontsize=16)
    plt.ylabel('Minutes_played',fontsize=16)
    plt.title('Goals Vs Minutes_played',fontsize=20)
    plt.show()



def DataVisualisation():
    while True:
        print("-"*80)
        print("|                                                               \t\t|")
        print('|\t\t<<<<<<< D A T A  V I S U A L I Z A T I O N >>>>>>>         \t|')
        print("|                                                               \t\t|")
        print('|\t\t1. Bar chart    > NUMBER OF GAMES PLAYED BY EACH PLAYER    \t|')
        print('|\t\t2. Histogram    > PLAYERS AND MINUTES PLAYED               \t|')
        print('|\t\t3. Scatter plot > GOALS Vs MINUTES PLAYED                  \t|')
        print('|\t\t4. HOME                                                    \t|')
        print("|                                                               \t\t|")
        print("-"*80)
        ch=int(input('Choose option :'))
        if ch ==1:
            BarPlayer()
        elif ch==2:
            HistPlayer()
        elif ch==3:
            ScatterPlot()
        elif ch==4:
            break
        else:
            print("Invalid option.Choose option 1 - 4")



def main():
    while True:
        print("-"*49)
        print("|                                      \t\t|")
        print('|\t\t<<<<<<< MAIN MENU >>>>>>>     \t|')
        print("|                                      \t\t|")
        print('|\t\t1. DATA VISUALIZATION         \t|')
        print('|\t\t2. DATA ANALYZATION           \t|')
        print('|\t\t3. CLOSE                      \t|')
        print("|                                      \t\t|")
        print("-"*49)
        ch=int(input('Choose option :'))
        if ch ==1:
            DataVisualisation()
        elif ch==2:
            DataAnalysis()
        elif ch==3:
            break
        else:
            print("Invalid option.Choose option 1 - 4")
        
        
main()
           
        


