# Cgpa-Queue

import java.io.*;
import java.util.*;
import java.math.*;
import java.text.*;
import java.util.regex.*;

class Student implements Comparable<Student>
{
	private int token;
	private String fname;
	private double cgpa;
	public Student(int id, String fname, double cgpa)
	{
		super();
		this.token = id;
		this.fname = fname;
		this.cgpa = cgpa;
	}
	public int getToken()
	{
		return token;
	}
	public String getFname() 
	{
		return fname;
	}
	public double getCgpa()
	{
		return cgpa;
	}
	
	@Override
	public int compareTo(Student stud2)
	{
		if(this.getCgpa()==stud2.getCgpa())
		{
			int i=this.fname.compareTo(stud2.getFname());
			if(i==0)
			{
				if(this.getToken()<stud2.getToken())
					return 1;
				else
					return -1;
			}
			else
				return i;
		}
		else if(this.getCgpa()<stud2.getCgpa())
			return 1;
		else
			return -1;
	}
}

public class Solution {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Scanner in = new Scanner(System.in);
		int totalEvents = Integer.parseInt(in.nextLine());
		PriorityQueue<Student> squeue = new PriorityQueue<>(totalEvents);
		while(totalEvents>0)
		{
			String event = in.next();
			if(event.equalsIgnoreCase("Served"))
			{
				if(!squeue.isEmpty())
					squeue.remove();
			}
			else
			{
				String name = in.next();
				Double cgpa = Double.parseDouble(in.next());
				int token = Integer.parseInt(in.next());
				Student stud = new Student(token,name,cgpa);
				
				squeue.add(stud);
			}
			totalEvents--;
		}
		Object[] sts = squeue.toArray();
		Arrays.sort(sts);
		if(squeue.isEmpty())
		{
			System.out.println("Empty");
		}
		else
		{
			for(int i = 0 ; i<sts.length;i++)
			{
				Student s=(Student) sts[i];
				System.out.println(s.getFname());
			}
		}
	}

}
