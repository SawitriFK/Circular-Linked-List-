# Circular-Linked-List-

#include<iostream>

class circq
{
    typedef struct node_
    {
        struct node_ *next;
        int info;
    }node;

    node *last;                         // ptr to last node of list

public:

    circq()                             // constructor
    {
        last = NULL;                    // reset last
    }

    bool isempty()
    {
        return last == NULL;
    }

    void enqueue(int q)
    {
        node *newNode=new node;         // new node
        newNode->info = q;
        if(last == NULL){               // if empty list
            last = newNode;             //  create single node list
            newNode->next = newNode;
            return;
        }                               // else
        newNode->next = last->next;     //  append node to end list
        last->next = newNode;
        last = newNode;
    }

    int dequeue()
    {
        if(last == NULL){               // check for empty list
            return 0;
        }
        node *first = last->next;       // set ptr to first node
        int x = first->info;            // set return value
        if(last->next == last)          // if single node
            last = NULL;                //  set list to empty
        else                            // else
            last->next = first->next;   //  advance first to next node
        delete first;                   // delete node
        return x;
    }

    ~circq()                            // destructor
    {
        while(!isempty())
            dequeue();
    }
};

int main()                              // test circq
{
circq cq;
    cq.enqueue(0);
    cq.enqueue(1);
    cq.enqueue(2);
    cq.enqueue(3);
    while(!cq.isempty())
        std::cout << cq.dequeue() << std::endl;
    return 0;
}
