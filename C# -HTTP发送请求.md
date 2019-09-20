# C# -HTTP发送请求



~~~c#
using System;
using System.Net;
using System.IO;
using System.Text;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Options;
using Newtonsoft.Json;

namespace ***
{
    public class HttpHelper
    {
        private static NLog.Logger logger = NLog.LoggerManager.GetCurrentClassLogger();

        public static string HttpGet(string url){
            var retString = string.Empty;
            try{
                HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
                request.Method = "Get";
                request.ContentType = "application/json;charset=UTF-8";
                request.Timeout = 10000;	//设置请求超时时间10s
                HttpWebResponse response = (HttpWebResponse)request.GetResponse();
                Stream myResponseStream = response.GetResponseStream();
                StreamReader myStreamReader = new StreamReader(myResponseStream, Encoding.UTF8);
                retString = myStreamRreader.ReadToEnd();
                myStreamReader.Close();
                myResponseStream.Close();
            }catch(Exception ex){
                logger.Error($"HttpGet异常：{ex.Message}");
            }

            return retString;
        }

        public static string HttpPost(string url, string data, string contentType = "application/json;charset=UTF-8"){
            var retString = string.Empty;
            try{
                HttpWebRequest request = (HttpWebRequest)WebRequest.Create(url);
                request.Method = "POST";
                request.ContentType = contentType;
                if (string.IsNullOrEmpty(data))
                   throw new Exception("请求体不能为空！");
                byte[] byteData = Encoding.UTF8.GetByte(data);
                using(Stream stream = request.GetRequestStream()){
                    stream.Write(byteData, 0, byteData,Length);
                }

                request.Timeout = 20000;
                HttpWebResponse response = (HttpResponse)request.GetResponse();
                Stream myResponseStream = response.GetResponseStream();
                StreamReader myStreamReader = new StreamReader(myResponseStream, Encoding.UTF8);
                retString = myStreamReader.ReadToEnd();
                myStreamReader.Close();
                myResponseStream.Close();
            }catch(Exception ex){
                logger.Error($"HttpPost异常：{ex.Message}");
            }

            return retString;
        }
    }
}
~~~







