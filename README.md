# gtk2
bonjour, j'ai un probleme au niveau toggle ne peux pas crochet merci
this is the code toggle can not work
#include <gtk/gtk.h>
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include "afficher.h"

void afficher(GtkWidget *pListView,int role)
{
enum {
CIN,
LOGIN,
PASSWORD,
ROLE,
TOGGLE_COLUMN,
N_COLUMN
};


GtkWidget  *window_ay4;

GtkWidget *pScrollbar;
GtkListStore *pListStore;
GtkTreeViewColumn *pColumn;
GtkCellRenderer *pCellRenderer;


FILE *f;char var[50],var1[50],var2[50];int var3;
f=fopen("/home/jbh/Projects/admin/src/user.txt","r");
void toggled_func(GtkCellRendererToggle *cell_renderer, gchar *path, gpointer user_data)
{
 
    GtkTreeIter iter;
    GtkTreePath *ppath;
    gboolean boolean;
 
 
// convertir la chaine path en GtkTreePath 
 
     ppath = gtk_tree_path_new_from_string (path);
 
// convertir la valeure recuperée en GtkTreeIter  
     gtk_tree_model_get_iter (GTK_TREE_MODEL (user_data),
                           &iter,
                           ppath);
//  utiliser la variable GtkTreeIter pour acceder la valeure booleaine                           
     gtk_tree_model_get (GTK_TREE_MODEL (user_data),
                           &iter,
                           TOGGLE_COLUMN,&boolean,
                           -1);
// changer cette valeure booleaine (! boolean )                          
     gtk_list_store_set (user_data, &iter,
                      TOGGLE_COLUMN, !boolean,
                      -1);
 
 
}

if (pListStore == NULL) {

pCellRenderer = gtk_cell_renderer_text_new();
pColumn = gtk_tree_view_column_new_with_attributes("cin",pCellRenderer,"text", CIN,NULL);

gtk_tree_view_append_column(GTK_TREE_VIEW(pListView), pColumn);

pCellRenderer = gtk_cell_renderer_text_new();
pColumn = gtk_tree_view_column_new_with_attributes("login",
pCellRenderer,
"text", LOGIN,
NULL);

gtk_tree_view_append_column(GTK_TREE_VIEW(pListView), pColumn);

pCellRenderer = gtk_cell_renderer_text_new();
pColumn = gtk_tree_view_column_new_with_attributes("password",
pCellRenderer,
"text", PASSWORD,
NULL);
gtk_tree_view_append_column(GTK_TREE_VIEW(pListView), pColumn);

pCellRenderer = gtk_cell_renderer_text_new();
pColumn = gtk_tree_view_column_new_with_attributes("role",
pCellRenderer,
"text", ROLE,
NULL);
gtk_tree_view_append_column(GTK_TREE_VIEW(pListView), pColumn);

pCellRenderer = gtk_cell_renderer_toggle_new();
pColumn=gtk_tree_view_column_new_with_attributes("select",pCellRenderer,"active", TOGGLE_COLUMN,
NULL);

gtk_tree_view_append_column(GTK_TREE_VIEW(pListView), pColumn);

}

pListStore = gtk_tree_view_get_model(GTK_TREE_VIEW(pListView));
pListStore=gtk_list_store_new(N_COLUMN, G_TYPE_STRING, G_TYPE_STRING, G_TYPE_STRING, G_TYPE_INT, G_TYPE_BOOLEAN);


while(fscanf(f,"%s %s %s %d",var,var1,var2,&var3)!=EOF)
	{

if (role!=var3)
continue;

GtkTreeIter pIter;

gtk_list_store_append(pListStore, &pIter);
gtk_list_store_set(pListStore, &pIter,CIN,var,LOGIN,var1,PASSWORD,var2,ROLE,var3,TOGGLE_COLUMN,FALSE,-1);
	}



fclose(f);
gtk_tree_view_set_model(GTK_TREE_VIEW(pListView),GTK_TREE_MODEL(pListStore)); 
g_object_unref(pListStore);	
}
