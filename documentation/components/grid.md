# Grid

### Overview

Grid is a control that contains a list organized by columns, where each column can receive an individual size and an alignment.

### Source Code

```java
import totalcross.sys.Settings;
import totalcross.ui.Button;
import totalcross.ui.Grid;
import totalcross.ui.MainWindow;
import totalcross.ui.dialog.MessageBox;
import totalcross.util.UnitsConverter;
import java.util.ArrayList;

public class GridSample extends MainWindow {

    private final int H = 225;
    private ArrayList<User> users = new ArrayList<>();
    private Grid grid;
    private Button loadButton;
    private int GAP = UnitsConverter.toPixels(DP + 8);
    
    public GridSample(){
        setUIStyle(Settings.Material);
    }

    @Override
    public void initUI() {
        String[] gridCaptions = { "Name", "Phone", "Email" };
        int gridWidths[] = { -35, -35, -30 };
        int gridAligns[] = { LEFT, LEFT, LEFT };

        grid = new Grid(gridCaptions, gridWidths, gridAligns, false);
        grid.verticalLineStyle = Grid.VERT_LINE;

        loadButton = new Button("Load");

        add(grid, LEFT + GAP, TOP + GAP, FILL - GAP, FILL - GAP * 9);
        add(loadButton, LEFT + GAP, BOTTOM - GAP, FILL - GAP, PREFERRED);

        loadButton.addPressListener( e -> {

            for (int i = 0; i < 5; i++) {
                users.add(new User("Joao ","99999999","joao@j.com","12345678"));
            }

            if (users.size() > 0) {
                String items[][] = new String[users.size()][3];
                for (int i = 0; i < users.size(); i++) {
                    User user = users.get(i);
                    items[i] = new String[] { user.getName(), user.getPhone(), user.getMail() };
                }
                grid.setItems(items);
            } else {
                MessageBox mb = new MessageBox("Message", "No registered users.", new String[] { "Close" });
                mb.popup();
            }
        });
    }

    public class User {

        private String name;
        private String phone;
        private String mail;
        private String password;

        public User() {

        }

        public User(String name, String phone, String mail, String password) {
            this.name = name;
            this.phone = phone;
            this.mail = mail;
            this.password = password;
        }

        public String getName() {
            return name;
        }
        public void setName(String name) {
            this.name = name;
        }
        public String getPhone() {
            return phone;
        }
        public void setPhone(String phone) {
            this.phone = phone;
        }
        public String getMail() {
            return mail;
        }
        public void setMail(String mail) {
            this.mail = mail;
        }
        public String getPassword() {
            return password;
        }
        public void setPassword(String password) {
            this.password = password;
        }

    }
}


```

### Methods



<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Constructor</b>
      </td>
      <td style="text-align:left">Grid(String[] captions, int[] widths, int[] aligns, boolean checkEnabled)</td>
      <td
      style="text-align:left">
        <p>Captions for the columns. Cannot be null;</p>
        <p></p>
        <p>Widths of the columns. If the total width is less than the grid&apos;s
          width,
          <br />the last column will fill until the grid width;</p>
        <p></p>
        <p>Alignment of information on the given column;</p>
        <p></p>
        <p>checkEnabled is True if you want the multi-selection check column;</p>
        <p></p>
        </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Constructor</b>
      </td>
      <td style="text-align:left">Grid(String[] captions, boolean checkEnabled)</td>
      <td style="text-align:left">
        <p>Captions for the columns;
          <br />checkEnabled is True if you want the multi-selection check column;</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">setItems(String[][] items)</td>
      <td style="text-align:left">Sets the grid items to be displayed.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">setDataSource(DataSource ds, int nrItems)</td>
      <td style="text-align:left">Sets the data source of this grid to be the given one.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">add(String[] item)</td>
      <td style="text-align:left">Add a new line.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Void</b>
      </td>
      <td style="text-align:left">add(String[] item, int row)</td>
      <td style="text-align:left">Add a new line at the given index position of the grid.</td>
    </tr>
  </tbody>
</table>

‌

### References <a id="references"></a>

* See the [github](https://github.com/TotalCross/TCSample/blob/master/src/main/java/totalcross/sample/components/ui/GridSample.java) sample.
* See the [Java Docs](https://rs.totalcross.com/doc/totalcross/ui/Grid.html) for more information.

