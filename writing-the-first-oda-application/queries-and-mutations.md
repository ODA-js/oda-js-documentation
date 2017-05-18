## Queries and Mutations

1. Open your browser and go by link: [localhost:3003/graphiq](http://localhost:3003/graphiq)<br>
2. GraphiQL editor will be opened. You can create graphql-queries using this editor. You can read more about GraphQL [here](http://graphql.org/learn/)<br>
Here's an example of how GraphiQL editor window will look like with added queries and server output.<br>
![](/assets/356.png)<br>
3. Insert graphql-queries in left block of editor (you can use test mutations and queries from **"Mutations"** and **"Queries"** sections).<br>
4. Click "Run query" button (the round one) and choose one of available queries.<br>
5. The result of the query will be displayed in the right block.<br>
6. Click 'Docs' button if you want to see the documentation about mutations and queries.<br>

### Mutations
'Mutation' - list of all actions, that you can do with your models (create, delete, update, assign, reassign).<br>
For example: let's add add mutation **"createStudent"**:


```
mutation createStudent{
  createStudent(input:{
    firstName: "StudentName",
    lastName: "StudentLasname",
    uin: "jiherig-4fj98734-c8h78-erfr"
  }) {
    student {
      node {
        id
        firstName
        lastName
      }
    }
  }
}
```
### Queries
'Queries' - list of all queries to your models. For example, create query 'getStudents':<br>


```
query getStudents{
  students(first:20) {
    edges {
      node {
        id
        firstName
        lastName
      }
    }
  }
}

```
The result of this request will be a list of first 20 students, registered in system.<br>

### Using cURL for queries
cURL is  a  tool  to  transfer data from or to a server, using one of the supported protocols (DICT,FILE, FTP, FTPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP,SFTP,SMTP, SMTPS, TELNET and TFTP).<br>
The command is designed to work without user interaction.<br>
For using cURL for queries, do this:<br>
1. Open new terminal window;<br>
2. Paste the query using the following syntax (for example, take the query to get 20 students from the "Query" section above):<br> 
`curl -X POST -H "Content-Type: application/json" -d '{"query": "{ students(first:20) {edges {node {id firstName lastName}}}}"}' http://localhost:3003/graphql`
3. Push 'Enter' button and check the result of the query. 
* If there's no students registered in system, the result of the query will look like this:<br>
![](/assets/img1245.png)<br>
* If there are any students registered in system, the result of the query will look like this:<br>
![](/assets/56.png)<br><br>

### Using WEB tools for queries
For using WEB tools for queries do this:<br>

1. Open your web browser and go to [http://localhost:3003](http://localhost:3003);
2. Open web inspector.
3. Go to console tab and add the query with following syntax to console:<br>

```
var xhr = new XMLHttpRequest();
      xhr.responseType = 'json';
      xhr.open('POST', '/graphql');
      xhr.setRequestHeader('Content-Type', 'application/json');
      xhr.setRequestHeader('Accept', 'application/json');
      xhr.onload = function () {
        console.log('data returned:', xhr.response);
      }
      xhr.send(JSON.stringify({query: "{ students(first:20) {edges {node {id firstName lastName}}} }"}));
```<br>

4. Push 'Enter' button and check the result of the query in console output.<br> 
* If there's no students registered in system, the result of the query will look like this:<br>
![](/assets/img1246.png)<br>
* If there are any students registered in system, the result of the query will look like this:<br>
For the example used, the result of the query will look like this:<br> ![](/assets/8989.png)