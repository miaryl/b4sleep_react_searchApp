# Search App with React
making super simple search app watching you tube

## 1. get infomation from [json placeholder](https://jsonplaceholder.typicode.com/)

  get user name and email address from fake api and show
 ```
function App() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => {
        return res.json();
      })
      .then((data) => setUsers(data));
  }, []);

  console.log(users);

  return (
    
      <div className="App">
        <div className="main">
          <h2>SEARCH APP</h2>
          <input type="text" />
          <div className="content">
            {users.map((user) => (
              <div className="box">
                <h3>{user.name}</h3>
                <hr />
                <p>{user.email}</p>
              </div>
            ))}
          </div>
        </div>
      </div>
    
  );
}`
```
* in this moment, not work search bar,
just show infos from fake api


<img width="1031" height="445" alt="Screenshot 2025-08-22 001611" src="https://github.com/user-attachments/assets/4adf8617-ccd0-4b51-86b5-cd290cbe940b" />

## 2. filtering function 
with `**`, new code

```
function App() {
  const [users, setUsers] = useState([]);
  **const [searchQuery, setSearchQuery] = useState([]);
  **const ref = useRef();

  **const handleSearch = () => {
    console.log(ref.current.value);

    // add filter function
    setSearchQuery(
      users.filter((user) =>
        user.name.toLowerCase().includes(ref.current.value)
      )
    );
  };

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => {
        return res.json();
      })
      .then((data) => setUsers(data));
  }, []);

  console.log(users);

  return (
    <div className="App">
      <div className="main">
        <h2>SEARCH APP</h2>
       ** <input type="text" ref={ref} onChange={() => handleSearch()} />
        <div className="content">
          **{searchQuery.map((user) => (
            <div className="box" key={user.id}>
              <h3>{user.name}</h3>
              <hr />
              <p>{user.email}</p>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
}
```
<img width="1017" height="279" alt="Screenshot 2025-08-22 003649" src="https://github.com/user-attachments/assets/c94d4a26-7913-4742-bd7c-b1ffbf6f73cb" />

YES! it works!
