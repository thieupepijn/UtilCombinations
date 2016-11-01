using System;
using System.Text;
using System.Collections.Generic;
using System.Linq;
namespace MiniCSharp
{
    public class UtilCombinations
    {
        public static bool Oplopend(string zin)
        {
            int lastnumber = -1;
            int number;
            for (int t=0;t<zin.Length;t++)
            {
                string letter = zin.Substring(t,1);
                number = Convert.ToInt32(letter);
                if (number < lastnumber)
                {
                    return false;
                }
                lastnumber = number;
            }
            return true;
        }
        public static string GenerateAllCombinations(string zin)
        {
            List<string> listResult = Combine(String.Empty, zin);
            listResult = listResult.OrderBy(z => z.Length).ToList();
            return List2String(listResult);
        }
        public static List<string> Combine(string zin, string others)
        {
            if (others.Length < 2)
            {
                return Combineer(zin, others);
            }
            else
            {
                List<string> listMain = Combineer(zin, others);;
                List<string> listAllChildren = new List<string>();
                for (int t=0;t<others.Length;t++)
                {
                    string  zinChild = zin + others.Substring(t,1);
                    string othersChild = others.Remove(t,1);
                    List<string> listChild = Combine(zinChild, othersChild);
                    listAllChildren.AddRange(listChild);
                }
                listMain.AddRange(listAllChildren);
                return listMain;
            }
        }
        public static List<string> Combineer(string zin, string others)
        {
            List<string> listReturn = new List<string>();
            for (int t=0;t<others.Length;t++)
            {
                string addZin = zin + others.Substring(t,1);
                if (Oplopend(addZin))
                {
                    listReturn.Add(addZin);
                }
            }
            return listReturn;
        }
        public static string List2String(List<string> listStrings)
        {
            if (listStrings == null)
            {
                return String.Empty;
            }
            else
            {
                StringBuilder sb = new StringBuilder();
                foreach (string stringetje in listStrings)
                {
                    sb.AppendLine(stringetje);
                }
                return sb.ToString();
            }
        }
        public static string DoStuff()
        {
            List<string> lijst = Combine("", "1234");
            return List2String(lijst);
        }
    }
}

































































































































































































































