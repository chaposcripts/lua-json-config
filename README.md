# lua-json-config
Make .json configs in Lua

## Usage
```lua
local JsonStatus, Json = pcall(require, 'jsoncfg');
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
