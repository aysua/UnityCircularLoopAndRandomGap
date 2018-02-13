# UnityCircularLoopAndRandomGap
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
//Comment section is previous trying(extended, huge, not good one).

public class ColumnScript : MonoBehaviour {

    private int index = 0;    
    private float firstpos;
    private GameObject[] column;
    public GameObject columnPrefab;
    public int columnSize;
    private Vector2 objectPoolPos = new Vector2(20, 0);
    public float speed;
    private float secondPos;
    //private bool setActiveAfterFirstGroup = false;

    void Start () 
    {
        column = new GameObject[columnSize];
        for (int i = 0; i < columnSize;i++ )//Initilizations
        {
            column[i] = (GameObject)Instantiate(columnPrefab, objectPoolPos, Quaternion.identity);
            column[i].GetComponent<Rigidbody2D>().velocity = Vector2.zero;        
        }
        column[index].GetComponent<Rigidbody2D>().velocity = new Vector2(-speed, 0f);//First movement
        firstpos = objectPoolPos.x;
   }

void Update () 
    {  /*      
       if (index >= columnSize-1)//Because of the giving movement to next array element
       {                
            column[0].transform.position = objectPoolPos;
            column[0].GetComponent<Rigidbody2D>().velocity = Vector2.zero;

            setActiveAfterFirstGroup = true;
            secondPos = column[index].GetComponent<Rigidbody2D>().position.x;//Last element's pos. Just before the 0th element

            if(index!=0)
            {                    
                float gap = Random.Range(3f, 11f);
                if (firstpos - secondPos >= gap)//gap between last and 0th element
                {
                    column[0].GetComponent<Rigidbody2D>().velocity = new Vector2(-speed, 0f);
                    index=0;                        
                }
            }
        }
        else
        {    
           if(setActiveAfterFirstGroup==true)
           {
                column[index + 1].transform.position = objectPoolPos;
                column[index + 1].GetComponent<Rigidbody2D>().velocity = Vector2.zero;
           }
        }
        */
           column[index + 1].transform.position = objectPoolPos;
           column[index + 1].GetComponent<Rigidbody2D>().velocity = Vector2.zero;
           if (index >= 0)
           { 
               secondPos = column[index].GetComponent<Rigidbody2D>().position.x; 
           }
           float gap = Random.Range(3f, 11f);
           if (firstpos - secondPos >= gap)
           {
               column[index+1].GetComponent<Rigidbody2D>().velocity = new Vector2(-speed, 0f);
               index++;
           }           
           
           if (index >= columnSize-1)
           {                             
               index = -1;
           }
           if(index==-1)
           {
               secondPos = column[columnSize-1].GetComponent<Rigidbody2D>().position.x;
           }
	}
}
