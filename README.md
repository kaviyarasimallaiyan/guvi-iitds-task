#Name:kaviyarasi.M
#Email:kavimallaiyan3@gmail.com
#Batch:D10
#task:to add new student


import mysql.connector
from mysql.connector.cursor import errors
import sys

def sql_connection():


    connection=mysql.connector.connect( host="localhost",user="root",password="",database="task")  
    return connection
    

def sql_insert(connection,inp_A,inp_B,inp_C,inp_D,inp_E,inp_F,inp_G,totalmark,average,grade):
    
    cursor=connection.cursor()
    sql="INSERT INTO task.student(Name,department,mark1,mark2,mark3,mark4,mark5,totalmark,average,grade) values (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"
    data=[inp_A,inp_B,inp_C,inp_D,inp_E,inp_F,inp_G,totalmark,average,grade]
    cursor.execute(sql,data)     
    connection.commit()
    connection.close()
    print("details added")
    

def grade(average):
    if(average>=95):
        return"A"
    elif(average>=90):
        return"B"
    elif(average>=75):
        return"C"
    elif(average>=60):
        return"D"
    else:
        return"F"

print("enter the option \n 1.add new student \n 2.get student \n 3.get all student \n 4.edit a student \n 5.exit")

inp_1=int(input("Enter the value:"))

if(inp_1==1):
    inp_A=input("Enter the Name :")
    inp_B=input("Enter the department:")
    inp_C=int(input("Enter mark1:"))
    inp_D=int(input("Enter mark2:"))
    inp_E=int(input("Enter mark3:"))
    inp_F=int(input("Enter mark4:"))
    inp_G=int(input("Enter mark5:"))

    totalmark=(inp_C+inp_D+inp_E+inp_F+inp_G)
    average=(inp_C+inp_D+inp_E+inp_F+inp_G)/5
    grade=grade(average)

    connection=sql_connection()
    sql_insert(connection,inp_A,inp_B,inp_C,inp_D,inp_E,inp_F,inp_G,totalmark,average,grade)

else:
    print("exit")