#include<stdio.h>
#define MAX_VERTEX_NUM 10
#define INFINITY 32768
#define Turn 1
#define False 0
#define Error -1
#define Ok 1
typedef enum{DG,DN,UDG,UDN}GraphKind;
typedef char VertexData;
typedef struct ArcNode
{
    int adj;
}ArcNode;
typedef struct
{
    VertexData vexs[MAX_VERTEX_NUM];
    ArcNode arcs[MAX_VERTEX_NUM][MAX_VERTEX_NUM];
    int vexnum,arcnum;
    GraphKind kind;
}AdjMatrix;
int LocateVertex(AdjMatrix *G,VertexData v)
{
    int j=Error,k;
    for(k=0;k<G->vexnum;k++)
        if(G->vexs[k]==v)
    {
        j=k;
        break;
    }
    return(j);
}
int CreateDN(AdjMatrix *G)
{
    int i,j,k,weight;
    VertexData v1,v2;
    printf("输入图的弧数和顶点数\n");
    fflush(stdin);
    scanf("%d,%d",&G->arcnum,&G->vexnum);
    for(i=0;i<G->vexnum;i++)
        for(j=0;j<G->vexnum;j++)
        G->arcs[i][j].adj=INFINITY;
for(i=0;i<G->vexnum;i++)
{
    printf("输入图的顶点\n");
    fflush(stdin);
    scanf("%c",&G->vexs[i]);//输入图的顶点
}
for(k=0;k<G->arcnum;k++)
{
    printf("输入一条弧的两个顶点和权值\n");
    fflush(stdin);
    scanf("%c,%c,%d",&v1,&v2,&weight);
    i=LocateVertex(G,v1);
    j=LocateVertex(G,v2);
    G->arcs[i][j].adj=weight;
}
return(Ok);
}
int CreateDG(AdjMatrix *G)
{
    int i,j,k;
    VertexData v1,v2;
    printf("输入图的弧数和顶点数\n");
    fflush(stdin);
    scanf("%d,%d",&G->arcnum,&G->vexnum);
    for(i=0;i<G->vexnum;i++)
        for(j=0;j<G->vexnum;j++)
        G->arcs[i][j].adj=0;
for(i=0;i<G->vexnum;i++)
{
    printf("输入图的顶点\n");
    fflush(stdin);
    scanf("%c",&G->vexs[i]);
}
for(k=0;k<G->arcnum;k++)
{
    printf("输入一条弧的两个顶点\n");
    fflush(stdin);
    scanf("%c,%c",&v1,&v2);
    i=LocateVertex(G,v1);
    j=LocateVertex(G,v2);
    G->arcs[i][j].adj=1;//建立弧
}
return(Ok);
}//
void printf_adjmatrix(AdjMatrix *G)
{
    int i,j;
    printf("  ");
    for(i=0;i<G->vexnum;i++)
    {
        printf("%c",G->vexs[i]);
        printf("   ");}
        printf("\n");
        for(i=0;i<G->vexnum;i++)
        {
            printf("%c ",G->vexs[i]);
            for(j=0;j<G->vexnum;j++)
            {
                if(G->arcs[i][j].adj==INFINITY)
                    printf("∞  ");
                else
                    printf("%-4d",G->arcs[i][j].adj);
            }
            printf("\n");

        }
    }
    int main()
    {
        AdjMatrix G;
        CreateDN(&G);
        printf_adjmatrix(&G);
        CreateDG(&G);
        printf_adjmatrix(&G);
    }
