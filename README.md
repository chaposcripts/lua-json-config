# lua-json-config
Make .json configs in Lua!  
Works with [MoonLoader](https://www.blast.hk/threads/13305/) or LuaJit + [json.lua](https://github.com/rxi/json.lua) only!

## Usage
```lua
local JsonStatus, Json = pcall(require, 'j-cfg');
assert(JsonStatus, 'jsoncfg.lua not found!');

local status, cfg = Json('myFirstConfig.json', {
    name = 'chapo',
    education = 'Electrical engineer',
    skills = {
        'shitcode'
    },
    body = {
        height = 190,
        weight = 70,
        age = 19,
        skinColor = 'white',
        eyesColor = 'blue',
        bodyParts = {
            'Head',
            'Left Hand',
            'Right Hand',
            'Left foot',
            'Right foot'
        }
    }
});

-- Read field
print(cfg.name);

-- Change field value
cfg.name = 'assadf';

-- Save config to file
cfg();
```

## Minified version
```lua
--// j-cfg by chapo (minified via https://goonlinetools.com/lua-minifier/)
local a,b=pcall(require,'json')local c={encode=encodeJson or(a and b.encode or nil),decode=decodeJson or(a and b.decode or nil)}assert(c.encode and c.decode,'error, cannot use json encode/decode functions. Install JSON cfg: https://github.com/rxi/json.lua')local function d(e)local f=io.open(e,'r')if f~=nil then io.close(f)end;return f~=nil end;function Json(g,h)local i,j,k={},false,'UNKNOWN_ERROR'local function l(m,n)local function o(p)local q=type(p)if q~='string'then p=tostring(p)end;local r=p:find('^(%d+)')or p:find('(%p)')or p:find('\\')or p:find('%-')return r==nil and p or('[%s]'):format(q=='string'and"'"..p.."'"or p)end;local s={'{'}local n=n or 0;for p,t in pairs(m)do table.insert(s,('%s%s = %s,'):format(string.rep("    ",n+1),o(p),type(t)=="table"and l(t,n+1)or(type(t)=='string'and"'"..t.."'"or tostring(t))))end;table.insert(s,string.rep('    ',n)..'}')return table.concat(s,'\n')end;local function u(h,v)local w=0;for x,y in pairs(h)do if v[x]==nil then if type(y)=='table'then v[x]={}_,subFilledCount=u(y,v[x])w=w+subFilledCount else v[x]=y;w=w+1 end elseif type(y)=='table'and type(v[x])=='table'then _,subFilledCount=u(y,v[x])w=w+subFilledCount end end;return v,w end;local function z(A)local B=io.open(g,'w')if B then local C,D=pcall(c.encode,A)if C and D then B:write(D)end;B:close()end end;local function E()local B=io.open(g,'r')if B then local F=B:read('*a')B:close()local G,H=pcall(c.decode,F)if G and H then i=H;j=true;local I,w=u(h,i)if w>0 then z(I)return I end;return H else k='JSON_DECODE_FAILED_'..H end else k='JSON_FILE_OPEN_FAILED'end;return{}end;if not d(g)then z(h)end;i=E()return j,setmetatable({},{__call=function(self,J)if type(J)=='table'then i=J;z(i)end end,__index=function(self,x)return x and i[x]or i end,__newindex=function(self,x,K)i[x]=K;z(i)end,__tostring=function(self)return l(i)end,__pairs=function()local x,y=next(i)return function()x,y=next(i,x)return x,y end end,__concat=function()return c.encode(i)end}),j and'ok'or k end;
local status, cfg = Json(...);
```
