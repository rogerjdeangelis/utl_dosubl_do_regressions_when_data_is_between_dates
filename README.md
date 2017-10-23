# utl_dosubl_do_regressions_when_data_is_between_dates
Given meta data with 3 date ranges, run three regression each with only dates in the respective date ranges

    ```  Given three date ranges exceute three 'proc reg'  with dates within the range                                                                                ```
    ```                                                                                                                                                               ```
    ```       Given three date ranges exceute three 'proc reg'  with dates within the range                                                                           ```
    ```                                                                                                                                                               ```
    ```       WORKING CODE                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```           set meta; * 3 date ranges for three regressions;  ie 21OCT2017-19DEC2017                                                                            ```
    ```                                                                14SEP2017-23DEC2017                                                                            ```
    ```           call symputx('start_date',put(start_date,8.));       14AUG2017-23JAN2018                                                                            ```
    ```           call symputx('end_date',put(end_date,8.));                                                                                                          ```
    ```                                                                                                                                                               ```
    ```           * run 3 separate regressions using the dates inside the meta data date ranges;                                                                      ```
    ```           rc = dosubl('                                                                                                                                       ```
    ```              proc reg data=have(where=( date ge &start_date and date le &end_date));                                                                          ```
    ```                 model invoice = mpg_city;                                                                                                                     ```
    ```              run;quit;                                                                                                                                        ```
    ```           ');                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```  see                                                                                                                                                          ```
    ```  https://goo.gl/762Hfd                                                                                                                                        ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/macro-to-perform-calculation-between-using-observations-that/m-p/406545                                  ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  HAVE                                                                                                                                                         ```
    ```  ====                                                                                                                                                         ```
    ```                                                                                                                                                               ```
    ```   WORK.META                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```       start_     end_                                                                                                                                         ```
    ```         date       date                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```    21OCT2017    19DEC2017    date in the regression data must in thiss range                                                                                  ```
    ```    14SEP2017    23DEC2017                                                                                                                                     ```
    ```    14AUG2017    23JAN2018                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```   WORK.HAVE                                                                                                                                                   ```
    ```                                                                                                                                                               ```
    ```        date     Invoice    MPG_City                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```    29SEP2017     $33,337       17    * only used in 2nd regression                                                                                            ```
    ```    23OCT2017     $33,873       16    * only used in 1st regression  ** see above                                                                              ```
    ```    15AUG2017     $32,244       20    * only used in 3rd regression                                                                                            ```
    ```                                                                                                                                                               ```
    ```    15OCT2017     $21,761       24                                                                                                                             ```
    ```    15SEP2017     $24,647       22                                                                                                                             ```
    ```    14OCT2017     $30,299       20                                                                                                                             ```
    ```    28SEP2017     $39,014       18                                                                                                                             ```
    ```                                                                                                                                                               ```
    ```   ....                                                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  *                _               _       _                                                                                                                   ```
    ```   _ __ ___   __ _| | _____     __| | __ _| |_ __ _                                                                                                            ```
    ```  | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |                                                                                                           ```
    ```  | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |                                                                                                           ```
    ```  |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data meta;                                                                                                                                                   ```
    ```   do _i_=1 to 3;                                                                                                                                              ```
    ```     start_date=today() - int(100*uniform(5731));                                                                                                              ```
    ```     end_date  =today() + int(100*uniform(5731));                                                                                                              ```
    ```     output;                                                                                                                                                   ```
    ```   end;                                                                                                                                                        ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  data have;                                                                                                                                                   ```
    ```     date=today() - int(100*uniform(1234));                                                                                                                    ```
    ```     set sashelp.cars(keep=invoice mpg_city);                                                                                                                  ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  data _null_;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     set meta;                                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```     call symputx('start_date',put(start_date,8.));                                                                                                            ```
    ```     call symputx('end_date',put(end_date,8.));                                                                                                                ```
    ```                                                                                                                                                               ```
    ```     rc = dosubl('                                                                                                                                             ```
    ```        proc reg data=have(where=( date ge &start_date and date le &end_date));                                                                                ```
    ```           model invoice = mpg_city;                                                                                                                           ```
    ```        run;quit;                                                                                                                                              ```
    ```     ');                                                                                                                                                       ```
    ```                                                                                                                                                               ```
    ```  run;quit;                                                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```

