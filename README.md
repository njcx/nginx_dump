## Nginx_dump    
    
    
    
    - 该工具用于把Openresty(Nginx+Lua) 请求参数和响应 dump出来，用于旁路HTTP流量分析、风控、资产识别、API数据泄露分析等等

    - 请在nginx.conf http 里面添加下面的片段，目录修改为实际目录
   
    - 目前是取的x-real-ip为客户ip， 代码位于 util的 _M.get_client_ip()，如果需要改为x-forwarded-for,修改
    local clent_ip = _M.req_x_real_ip() 为 local clent_ip = _M.req_xxf()

    - 日志文件目录 在config.lua 里面配置


    http {
    
        lua_package_path          "/usr/local/openresty/nginx/conf/nginx_dump/?.lua;;";
        init_by_lua_file          /usr/local/openresty/nginx/conf/nginx_dump/init.lua;
        init_worker_by_lua_file   /usr/local/openresty/nginx/conf/nginx_dump/init_worker.lua;
        access_by_lua_file        /usr/local/openresty/nginx/conf/nginx_dump/access.lua;
        body_filter_by_lua_file   /usr/local/openresty/nginx/conf/nginx_dump/body_filter.lua;      
    
        server {
                listen       443 ssl;
                server_name  localhost;
        }
    
    }
    
    
    
