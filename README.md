# MySQL_CSharp_Unity
This is a CSharp and Unity library that was designed based off of sqlite-net as an example. This approach makes it clean and easy to work with MySQL from your application without many headaches. To use this library just simply add the dependencies and mysql script to your project, and you're off to the races. Below are a couple examples of working with the library.

```
public class Accounts
{
  [PrimaryKey, LimitKey(17)] public string SteamID;
  public bool VacBanned;
}

public class Communication
{
  private MySQL mySQL;
  
  public void Connection(string address, string user, string pass, string database)
  {
    mySQL = new MySQL();
    mySQL.Connect(address, user, pass, database);
    mySQL.CreateTable<Accounts>();
    SetupAccount("12345678901234567", false);
  }

  private void SetupAccount(string steamID, bool vacBanned)
  {
    if (mySQL.Select<Accounts>(new[] { "SteamID" }, false, new[] { steamID }).Count == 0)
      mySQL.Insert(new Accounts
      {
          SteamID = steamID,
          VacBanned = vacBanned
      });
  }
} 
```

Reference to Sqlite-net
https://github.com/praeclarum/sqlite-net

*Note since this library was created in unity there will be sections that use Debug.Log("Message"); which will not work outside of unity. You can change these to Console.WriteLine("Message"); to produce the same result.
