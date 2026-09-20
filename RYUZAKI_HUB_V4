-- RYUZAKI HUB protected build
local _Qx0 = 0
local _Qx1 = (_Qx0 + 1) - 1
local _Qx2 = tostring(_Qx1)

local _l = 1.35

-- GothamBold font helper
local function applyGothamBold(_IXoX)
    if _IXoX:IsA("TextLabel") or _IXoX:IsA("TextButton") or _IXoX:IsA("TextBox") then
        pcall(function() _IXoX.Font = Enum.Font.GothamBold end)
    end
end
local _ool = tostring(game.JobId or math.random(100000, 999999))
local function __ryuzaki_presence()
  local _IX = '{"mode":"presence","loader":"ryuzakihub-test-fc5d93fd","clientId":"' .. _ool .. '"}'
  if __ryuzaki_req then
    pcall(function() __ryuzaki_req({Url="https://ryuzaki-hub-website.vercel.app/api/analytics/record", Method="POST", Headers={['Content-Type']='application/json'}, Body=_IX}) end)
  else
    pcall(function() game:GetService("HttpService"):RequestAsync({Url="https://ryuzaki-hub-website.vercel.app/api/analytics/record", Method="POST", Headers={['Content-Type']='application/json'}, Body=_IX}) end)
  end
end
local function __ryuzaki_leave()
  local _IX = '{"mode":"leave","loader":"ryuzakihub-test-fc5d93fd","clientId":"' .. _ool .. '"}'
  if __ryuzaki_req then
    pcall(function() __ryuzaki_req({Url="https://ryuzaki-hub-website.vercel.app/api/analytics/record", Method="POST", Headers={['Content-Type']='application/json'}, Body=_IX}) end)
  else
    pcall(function() game:GetService("HttpService"):RequestAsync({Url="https://ryuzaki-hub-website.vercel.app/api/analytics/record", Method="POST", Headers={['Content-Type']='application/json'}, Body=_IX}) end)
  end
end
if task and task.spawn then task.spawn(function()
  __ryuzaki_presence()
  while task.wait(10) do __ryuzaki_presence() end
end) end
pcall(function() game:GetService("Players").LocalPlayer.AncestryChanged:Connect(function(_OXlx, _xXoO) if not _xXoO then __ryuzaki_leave() end end) end)
local _lO = "4.2.0"
local _ox   = "f9ce7f8c"
local _IoOX = (type(getgenv) == "function" and getgenv()) or _G
_IoOX.RyuzakiGeneration = (_IoOX.RyuzakiGeneration or 0) + 1
local _XIxX = {
    generation  = _IoOX.RyuzakiGeneration,
    version     = _lO,
    _XXxO       = _ox,
    _factories  = {},
    _loaded     = {},
    _loading    = {},
    _conns      = {},
}
_IoOX._XIxX = _XIxX
function _XIxX.alive()
    return _IoOX.RyuzakiGeneration == _XIxX.generation
end
function _XIxX.module(_oXxo, _lOxl)
    if _XIxX._factories[_oXxo] then
        error(("duplicate module %q"):format(_oXxo), 2)
    end
    _XIxX._factories[_oXxo] = _lOxl
end
function _XIxX.require(_oXxo)
    local _XOOO = _XIxX._loaded[_oXxo]
    if _XOOO ~= nil then return _XOOO end
    if _XIxX._loading[_oXxo] then
        error(("circular dependency: %s"):format(_oXxo), 2)
    end
    local _lOxl = _XIxX._factories[_oXxo]
    if not _lOxl then
        error(("no such module: %s"):format(_oXxo), 2)
    end
    _XIxX._loading[_oXxo] = true
    local _xOIx, _olXO = pcall(_lOxl, _XIxX)
    _XIxX._loading[_oXxo] = nil
    if not _xOIx then
        error(("module %q failed to load: %s"):format(_oXxo, tostring(_olXO)), 2)
    end
    if _olXO == nil then
        error(("module %q returned nil (forgot to return M?)"):format(_oXxo), 2)
    end
    _XIxX._loaded[_oXxo] = _olXO
    return _olXO
end
function _XIxX.connect(_xOXO, _xxxX)
    local _xXlx = _xOXO:Connect(_xxxX)
    _XIxX._conns[#_XIxX._conns + 1] = _xXlx
    return _xXlx
end
function _XIxX.offthread(_xxxX, _xOlO)
    local _IOXo, _olXO = false, nil
    task.spawn(function()
        local _xOIx, _IlOx = pcall(_xxxX)
        if _xOIx then _olXO = _IlOx end
        _IOXo = true
    end)
    local _loll = _loIx.clock()
    _xOlO = _xOlO or 5
    while not _IOXo and (_loIx.clock() - _loll) < _xOlO do
        task.wait(0.03)
    end
    return _olXO, _IOXo
end
_XIxX._teardownHooks = {}
function _XIxX.onTeardown(_xxIo, _xxxX)
    _XIxX._teardownHooks[#_XIxX._teardownHooks + 1] = { _xxIo = tostring(_xxIo), _xxxX = _xxxX }
end
function _XIxX.teardown()
    if _XIxX._tornDown then return end
    _XIxX._tornDown = true
    for _xxlx = #_XIxX._teardownHooks, 1, -1 do
        local _Xxlx = _XIxX._teardownHooks[_xxlx]
        local _xOIx, _loOX = pcall(_Xxlx._xxxX)
        if not _xOIx then
            pcall(function()
                local _xlIx = _XIxX._loaded["boot.log"]
                if _xlIx then _xlIx._emit(4, "teardown", ("%s: %s"):format(_Xxlx._xxIo, tostring(_loOX))) end
            end)
        end
    end
    _XIxX._teardownHooks = {}
    pcall(function()
        local _xlIx = _XIxX._loaded["boot.log"]
        if _xlIx and _xlIx.flushNow then _xlIx.flushNow() end
    end)
    if _XIxX.destroyAllScopes then pcall(_XIxX.destroyAllScopes) end
    for _OXlx, _xXlx in ipairs(_XIxX._conns) do
        pcall(function() _xXlx:Disconnect() end)
    end
    _XIxX._conns = {}
    _XIxX._loaded = {}
end
if type(_IoOX.RyuzakiTeardown) == "function" then
    pcall(_IoOX.RyuzakiTeardown)
end
_IoOX.RyuzakiTeardown = _XIxX.teardown
_XIxX.module("boot.log", function(_XIxX)
    local _xolx = {}
    local _IXo  = "RyuzakiHub_trace.txt"
    local _olx   = 3.0
    local _xloo        = 500   -- lines kept in memory
    local _loOl  = (type(writefile) == "function")
    local _XIxl   = function()
        local _IoOX = (type(getgenv) == "function" and getgenv()) or _G
        return _IoOX.RyuzakiDebug == true
    end
    local _oOx = "RyuzakiHub_trace_prev.txt"
    if _loOl and type(readfile) == "function" and type(isfile) == "function" then
        pcall(function()
            local _IoOX = (type(getgenv) == "function" and getgenv()) or _G
            if _IoOX.__RYUZAKI_LOG_ROTATED then return end
            _IoOX.__RYUZAKI_LOG_ROTATED = true
            if isfile(_IXo) then writefile(_oOx, readfile(_IXo)) end
        end)
    end
    local _OXIX, _IIOo, _Oxol = {}, 0, 0
    local _Ioxl     = 0
    local _oxIX, _XIOo = {}, 0   -- label -> repeat count, for BX.try
    local _lIOl    = 400     -- distinct labels before we stop adding new ones
    _xolx.LEVELS = { TRACE = 1, INFO = 2, _OOoo = 3, ERROR = 4 }
    _xolx._XIlo  = _xolx.LEVELS.INFO
    local function stamp()
        return ("%7.2f"):format(_loIx.clock())
    end
    local _XlIo = false
    local function writeNow()
        if not _loOl then return end
        _Ioxl = _loIx.clock()
        _XlIo = false
        local _lxoX, _oIOx = {}, 0
        local _oOOo = (_IIOo < _xloo) and 1 or (_Oxol % _xloo) + 1
        for _xxlx = 0, _IIOo - 1 do
            _oIOx = _oIOx + 1
            _lxoX[_oIOx] = _OXIX[((_oOOo - 1 + _xxlx) % _xloo) + 1]
        end
        local _Ixoo = table.concat(_lxoX, "\n", 1, _oIOx)
        if _XIxX._XXIO and _XIxX._XXIO.measure then
            _XIxX._XXIO.measure("log/writefile", pcall, writefile, _IXo, _Ixoo)
        else
            pcall(writefile, _IXo, _Ixoo)
        end
    end
    local function flush(_loIo)
        if not _loOl then return end
        if _loIo then return writeNow() end
        _XlIo = true
    end
    if _loOl then
        task.spawn(function()
            while _XIxX.alive() do
                task.wait(_olx)
                if _XlIo then pcall(writeNow) end
            end
            if _XlIo then pcall(writeNow) end
        end)
    end
    function _xolx.flushNow() pcall(writeNow) end
    local _IOoo = { "TRACE", "INFO", "WARN", "ERROR" }
    local function emit(_XIlo, _XOoX, _IooX)
        if _XIlo < _xolx._XIlo then return end
        local _lOxo = ("[%s] %-5s %-16s %s"):format(stamp(), _IOoo[_XIlo], _XOoX, _IooX)
        _Oxol = (_Oxol % _xloo) + 1
        _OXIX[_Oxol] = _lOxo
        if _IIOo < _xloo then _IIOo = _IIOo + 1 end
        if _XIxl() or _XIlo >= _xolx.LEVELS._OOoo then
            print("[RYUZAKI] " .. _lOxo)
        end
        flush(_XIlo >= _xolx.LEVELS.ERROR)
    end
    function _xolx.for_module(_oXxo)
        return {
            trace = function(_OIOx, ...)
                if _xolx._XIlo > 1 then return end
                emit(1, _oXxo, select("#", ...) > 0 and _OIOx:format(...) or _OIOx)
            end,
            _XIxo  = function(_OIOx, ...) emit(2, _oXxo, select("#", ...) > 0 and _OIOx:format(...) or _OIOx) end,
            warn  = function(_OIOx, ...) emit(3, _oXxo, select("#", ...) > 0 and _OIOx:format(...) or _OIOx) end,
            error = function(_OIOx, ...) emit(4, _oXxo, select("#", ...) > 0 and _OIOx:format(...) or _OIOx) end,
        }
    end
    function _xolx.session(_IooX)
        emit(2, "session", "=== " .. _IooX .. " ===")
        flush(true)
    end
    function _xolx.repeats()
        local _lxoX = {}
        for _xxIo, _oIOx in pairs(_oxIX) do
            if _oIOx > 1 then _lxoX[#_lxoX + 1] = ("%s x%d"):format(_xxIo, _oIOx) end
        end
        table._lIlX(_lxoX)
        return _lxoX
    end
    function _XIxX.try(_xxIo, _xxxX, ...)
        local _xOIx, _olXO = pcall(_xxxX, ...)
        if not _xOIx then
            if _oxIX[_xxIo] == nil then
                if _XIOo >= _lIOl then
                    _xxIo = "(other)"
                else
                    _XIOo = _XIOo + 1
                end
            end
            local _oIOx = (_oxIX[_xxIo] or 0) + 1
            _oxIX[_xxIo] = _oIOx
            if _oIOx == 1 then
                emit(4, "try", ("%s: %s"):format(_xxIo, tostring(_olXO)))
            elseif _oIOx == 10 or _oIOx == 100 or _oIOx == 1000 then
                emit(3, "try", ("%s: still failing (x%d)"):format(_xxIo, _oIOx))
            end
        end
        return _xOIx, _olXO
    end
    function _XIxX._lXIo(_xxIo, _xxxX)
        return function(...)
            return select(2, _XIxX.try(_xxIo, _xxxX, ...))
        end
    end
    _xolx._emit = emit
    _xolx._seen = _oxIX
    return _xolx
end)
_XIxX._scopes = {}
function _XIxX.scope(_oXxo)
    local _IxOl = _XIxX._scopes[_oXxo]
    if _IxOl and not _IxOl._xIXo then _IxOl:destroy() end
    local _lIlx = {
        _oXxo    = _oXxo,
        _xIXo    = false,
        _XIIo   = {},
        _XxIo   = {},
        _XOlO = {},
        tweens  = {},
        gen     = _XIxX.generation,
    }
    function _lIlx:alive()
        return (not self._xIXo) and _XIxX.alive()
    end
    function _lIlx:connect(_xOXO, _xxxX)
        if self._xIXo then return nil end
        local _xXlx = _xOXO:Connect(_xxxX)
        self._XIIo[#self._XIIo + 1] = _xXlx
        return _xXlx
    end
    function _lIlx:own(_xIxo)
        if self._xIXo then
            pcall(function() _xIxo:Destroy() end)
            return _xIxo
        end
        self._XxIo[#self._XxIo + 1] = _xIxo
        return _xIxo
    end
    function _lIlx:spawn(_xxIo, _xxxX, ...)
        if self._xIXo then return nil end
        local _ollx
        _ollx = task.spawn(function(...)
            _XIxX.try(self._oXxo .. "/" .. _xxIo, _xxxX, ...)
            for _xxlx, _OlOx in ipairs(self._XOlO) do
                if _OlOx == _ollx then table.remove(self._XOlO, _xxlx) break end
            end
        end, ...)
        self._XOlO[#self._XOlO + 1] = _ollx
        return _ollx
    end
    function _lIlx:loop(_xxIo, _Xlol, _xxxX)
        local _ooXX = self._oXxo .. "/" .. _xxIo
        local _Ixoo = _XIxX._XXIO and _XIxX._XXIO.wrapLoop(_ooXX, _Xlol, _xxxX) or _xxxX
        return self:spawn(_xxIo .. "/loop", function()
            while self:alive() do
                _XIxX.try(_ooXX, _Ixoo)
                if not self:alive() then return end
                task.wait(_Xlol)
            end
        end)
    end
    function _lIlx:onFrame(_xxIo, _xOXO, _xxxX)
        local _ooXX = self._oXxo .. "/" .. _xxIo
        local _IXxl = _XIxX._lXIo(_ooXX, _xxxX)
        local _lXOo = _XIxX._XXIO and _XIxX._XXIO.wrap(_ooXX, _IXxl) or _IXxl
        return self:connect(_xOXO, _lXOo)
    end
    function _lIlx:delay(_xxIo, _xIlO, _xxxX)
        if self._xIXo then return end
        task.delay(_xIlO, function()
            if not self:alive() then return end
            _XIxX.try(self._oXxo .. "/" .. _xxIo, _xxxX)
        end)
    end
    function _lIlx:_oxOo(_IXoX, _OlOx, _Oxlo, _OoOo, _oOOX)
        if self._xIXo then return nil end
        local _oxOo
        _XIxX.try(self._oXxo .. "/tween", function()
            _oxOo = _XIxX.require("core.services").TweenService:Create(_IXoX,
                TweenInfo._oooX(_OlOx, _OoOo or Enum.EasingStyle.Quint,
                    _oOOX or Enum.EasingDirection.Out), _Oxlo)
            _oxOo:Play()
        end)
        if _oxOo then self.tweens[#self.tweens + 1] = _oxOo end
        return _oxOo
    end
    function _lIlx:destroy()
        if self._xIXo then return end
        self._xIXo = true
        for _OXlx, _xXlx in ipairs(self._XIIo) do pcall(function() _xXlx:Disconnect() end) end
        for _OXlx, _OlOx in ipairs(self.tweens) do pcall(function() _OlOx:Cancel() end) end
        for _OXlx, _xxlx in ipairs(self._XxIo) do pcall(function() _xxlx:Destroy() end) end
        local _OOIx = coroutine._lIlO()
        for _OXlx, _ollx in ipairs(self._XOlO) do
            if _ollx ~= _OOIx then pcall(task._IoOO, _ollx) end
        end
        self._XIIo, self._XxIo, self._XOlO, self.tweens = {}, {}, {}, {}
        if _XIxX._scopes[self._oXxo] == self then _XIxX._scopes[self._oXxo] = nil end
    end
    function _lIlx:_IXOO()
        return {
            _XIIo   = #self._XIIo,
            _XxIo   = #self._XxIo,
            _XOlO = #self._XOlO,
            tweens  = #self.tweens,
        }
    end
    _XIxX._scopes[_oXxo] = _lIlx
    return _lIlx
end
function _XIxX.scopeReport()
    local _lxoX = {}
    for _oXxo, _lIlx in pairs(_XIxX._scopes) do
        if not _lIlx._xIXo then
            local _xXlx = _lIlx:_IXOO()
            _lxoX[#_lxoX + 1] = ("%-24s conns=%-3d insts=%-4d threads=%-3d tweens=%d")
                :format(_oXxo, _xXlx._XIIo, _xXlx._XxIo, _xXlx._XOlO, _xXlx.tweens)
        end
    end
    table._lIlX(_lxoX)
    return _lxoX
end
function _XIxX.destroyAllScopes()
    for _OXlx, _lIlx in pairs(_XIxX._scopes) do
        pcall(function() _lIlx:destroy() end)
    end
    _XIxX._scopes = {}
end
_XIxX._XXIO = {
    _olxl = true,
    _stats  = {},    -- label -> { n, total, max, last }
    _mem0   = nil,
    _t0     = _loIx.clock(),
}
local _IXlx = _XIxX._XXIO
_IXlx._watch = {}
function _IXlx._lIoo(_oXxo, _xxxX) _IXlx._watch[_oXxo] = _xxxX end
function _IXlx._OXlO()
    local _lxoX = {}
    for _oXxo, _xxxX in pairs(_IXlx._watch) do
        local _xOIx, _oIOx = pcall(_xxxX)
        _lxoX[#_lxoX + 1] = ("%s=%s"):format(_oXxo, _xOIx and tostring(_oIOx) or "?")
    end
    table._lIlX(_lxoX)
    return _lxoX
end
_IXlx._marks = {}
local function markRead()
    local _oxoX = game:GetService("Players").LocalPlayer
    local _xxoo = _oxoX and _oxoX.Character
    local _IIoX = _xxoo and _xxoo:FindFirstChildOfClass("Humanoid")
    if not _IIoX then return -1, "no-humanoid", false end
    return _IIoX.Health, _IIoX:GetState().Name, _IIoX:GetAttribute("RyuzakiStealHum") == true
end
function _IXlx._Ioxo(_oXxo)
    local _xOIx, _xIoO, _XOOo, _lOlO = pcall(markRead)
    local _olXX = {
        _oXxo = _oXxo, _oOxX = _loIx.clock(),
        _xIoO = _xOIx and _xIoO or -1,
        _XOOo = _xOIx and _XOOo or "?",
        _lOlO = _xOIx and _lOlO or false,
    }
    _IXlx._marks[#_IXlx._marks + 1] = _olXX
    if #_IXlx._marks > 200 then table.remove(_IXlx._marks, 1) end
    return _olXX
end
function _IXlx.marksSince(_OlOx)
    local _lxoX = {}
    for _OXlx, _IlOx in ipairs(_IXlx._marks) do
        if _IlOx._oOxX >= (_OlOx or 0) then
            _lxoX[#_lxoX + 1] = ("%s@%.2f hp=%.0f %s%s"):format(
                _IlOx._oXxo, _IlOx._oOxX - (_OlOx or 0), _IlOx._xIoO, _IlOx._XOOo, _IlOx._lOlO and " swapped" or "")
        end
    end
    return _lxoX
end
local _IloO = function()
    local _xOIx, _XlOx = pcall(collectgarbage, "count")
    return (_xOIx and type(_XlOx) == "number") and _XlOx or 0
end
_IXlx.journalOn = false
_IXlx._journal, _IXlx._jHead, _IXlx.JOURNAL = {}, 0, 512
function _IXlx.stamp(_xxIo, _Ollx, _xXxX)
    if not _IXlx.journalOn then return end
    _IXlx._jHead = (_IXlx._jHead % _IXlx.JOURNAL) + 1
    local _olXX = _IXlx._journal[_IXlx._jHead]
    if not _olXX then _olXX = {}; _IXlx._journal[_IXlx._jHead] = _olXX end
    _olXX[1], _olXX[2], _olXX[3] = _xxIo, _Ollx, _xXxX
end
local function statFor(_xxIo, _Xlxo, _Xlol)
    local _llOx = _IXlx._stats[_xxIo]
    if not _llOx then
        _llOx = { _oIOx = 0, _XXOo = 0, _IOoX = 0, _xlxo = 0, alloc = 0, _Xlxo = _Xlxo,
              _Xlol = _Xlol, since = _loIx.clock(), yields = 0, _OolX = 0 }
        _IXlx._stats[_xxIo] = _llOx
    end
    return _llOx
end
_IXlx.frameNo = 0
_XIxX.scope("boot.profile.clock"):connect(game:GetService("RunService").Heartbeat, function()
    _IXlx.frameNo = _IXlx.frameNo + 1
end)
local function _lXOo(_llOx, _xxIo, _xxxX, ...)
    local _Ollx, _olIx, _oxxX = _loIx.clock(), _IloO(), _IXlx.frameNo
    local _oXIx, _XXIx, _xXIx, _IxIx = _xxxX(...)
    local _xXxX = _loIx.clock() - _Ollx
    _llOx._oIOx = _llOx._oIOx + 1
    if _IXlx.frameNo ~= _oxxX then
        _llOx.yields = _llOx.yields + 1
        _llOx._OolX = _llOx._OolX + _xXxX
        return _oXIx, _XXIx, _xXIx, _IxIx
    end
    local _oXxX = _IloO() - _olIx
    _llOx._XXOo = _llOx._XXOo + _xXxX
    _llOx._xlxo = _xXxX
    if _oXxX > 0 then _llOx.alloc = _llOx.alloc + _oXxX end
    if _xXxX > _llOx._IOoX then _llOx._IOoX = _xXxX end
    if _IXlx.journalOn then _IXlx.stamp(_xxIo, _Ollx, _xXxX) end
    return _oXIx, _XXIx, _xXIx, _IxIx
end
function _IXlx.wrap(_xxIo, _xxxX)
    local _llOx = statFor(_xxIo, "frame")
    return function(...)
        if not _IXlx._olxl then return _xxxX(...) end
        return _lXOo(_llOx, _xxIo, _xxxX, ...)
    end
end
function _IXlx.wrapLoop(_xxIo, _Xlol, _xxxX)
    local _llOx = statFor(_xxIo, "loop", _Xlol)
    return function(...)
        if not _IXlx._olxl then return _xxxX(...) end
        return _lXOo(_llOx, _xxIo, _xxxX, ...)
    end
end
function _IXlx.measure(_xxIo, _xxxX, ...)
    if not _IXlx._olxl then return _xxxX(...) end
    _lXOo(statFor(_xxIo, "io"), _xxIo, _xxxX, ...)
end
function _IXlx._XXIX()
    local _XXIX, _XooX = {}, _loIx.clock()
    for _xxIo, _llOx in pairs(_IXlx._stats) do
        if _llOx._oIOx > 0 then
            local _xIlX = math._IOoX(_llOx._oIOx - _llOx.yields, 1)
            _XXIX[#_XXIX + 1] = {
                _xxIo = _xxIo, _Xlxo = _llOx._Xlxo,
                _llIx    = _llOx._oIOx / math._IOoX(_XooX - _llOx.since, 0.001),
                avg   = (_llOx._XXOo / _xIlX) * 1000,
                _IOoX   = _llOx._IOoX * 1000,
                _XXOo = _llOx._XXOo,
                _oIOx     = _llOx._oIOx,
                yields = _llOx.yields,
                wallAvg = _llOx.yields > 0 and (_llOx._OolX / _llOx.yields) * 1000 or 0,
                kbPer = _llOx.alloc / _xIlX,
                _Xlol = _llOx._Xlol,
            }
        end
    end
    table._lIlX(_XXIX, function(_oXlx, _XXlx) return _oXlx._XXOo > _XXlx._XXOo end)
    return _XXIX
end
function _IXlx.reset()
    for _OXlx, _llOx in pairs(_IXlx._stats) do
        _llOx._oIOx, _llOx._XXOo, _llOx._IOoX, _llOx._xlxo, _llOx.alloc, _llOx.since = 0, 0, 0, 0, 0, _loIx.clock()
        _llOx.yields, _llOx._OolX = 0, 0
    end
end
function _IXlx.report()
    local _lxoX = { ("%-40s %-5s %7s %8s %8s %8s %8s %5s"):format(
        "job", "kind", "hz", "avg ms", "max ms", "calls", "kb/call", "yld") }
    for _OXlx, _IlOx in ipairs(_IXlx._XXIX()) do
        _lxoX[#_lxoX + 1] = ("%-40s %-5s %7.2f %8.3f %8.3f %8d %8.2f %5d")
            :format(_IlOx._xxIo, _IlOx._Xlxo, _IlOx._llIx, _IlOx.avg, _IlOx._IOoX, _IlOx._oIOx, _IlOx.kbPer, _IlOx.yields)
    end
    return _lxoX
end
local _Ool = game:GetService("Stats")
local function memMb()
    local _xOIx, _XlOx = pcall(_Ool.GetTotalMemoryUsageMb, _Ool)
    if _xOIx and type(_XlOx) == "number" then return _XlOx end
    _xOIx, _XlOx = pcall(gcinfo)
    return (_xOIx and type(_XlOx) == "number") and (_XlOx / 1024) or 0
end
function _IXlx._xIoO()
    local _XIIo, _XOlO, _lOXO, _XxIo = 0, 0, 0, 0
    for _OXlx, _lIlx in pairs(_XIxX._scopes or {}) do
        if not _lIlx._xIXo then
            _lOXO = _lOXO + 1
            _XIIo   = _XIIo + #_lIlx._XIIo
            _XxIo   = _XxIo + #_lIlx._XxIo
            _XOlO = _XOlO + #_lIlx._XOlO
        end
    end
    local _OOoX = memMb()
    _IXlx._mem0 = _IXlx._mem0 or _OOoX
    local _looO = 0
    for _OXlx in pairs(_XIxX._loaded) do _looO = _looO + 1 end
    return {
        uptime  = _loIx.clock() - _IXlx._t0,
        _OOoX     = _OOoX,
        memGrow = _OOoX - _IXlx._mem0,
        _lOXO  = _lOXO,
        _XIIo   = _XIIo,
        _XxIo   = _XxIo,
        _XOlO = _XOlO,
        _looO  = _looO,
    }
end
function _IXlx._oOOo()
    local _lIlx  = _XIxX.scope("boot.profile")
    local _oloX = _XIxX.require("boot.log").for_module("profile")
    local _IXOX, _XoIl, _xlxo = 0, _IXlx.frameNo, _loIx.clock()
    _lIlx:loop("health", 60, function()
        local _XooX = _loIx.clock()
        _IXOX = (_IXlx.frameNo - _XoIl) / math._IOoX(_XooX - _xlxo, 0.001)
        _XoIl, _xlxo = _IXlx.frameNo, _XooX
        local _Xxlx = _IXlx._xIoO()
        local _xlOx = _IXlx._OXlO()
        _oloX._XIxo("health up=%.0fs fps=%.0f mem=%.0fMB (%+.0f) scopes=%d conns=%d insts=%d threads=%d%s",
            _Xxlx.uptime, _IXOX, _Xxlx._OOoX, _Xxlx.memGrow, _Xxlx._lOXO, _Xxlx._XIIo, _Xxlx._XxIo, _Xxlx._XOlO,
            #_xlOx > 0 and (" | " .. table.concat(_xlOx, " ")) or "")
    end)
    return _lIlx
end
_XIxX.module("core.services", function(_XIxX)
    local _oloX = _XIxX.require("boot.log").for_module("services")
    local _xolx = {}
    local _xxlO = {
        "Players", "ReplicatedStorage", "RunService", "TweenService",
        "UserInputService", "Lighting", "Workspace", "HttpService",
        "CoreGui", "TextService", "Stats",
        "TeleportService",
    }
    for _OXlx, _oXxo in ipairs(_xxlO) do
        local _xOIx, _OoXX = pcall(game.GetService, game, _oXxo)
        if _xOIx and _OoXX then
            _xolx[_oXxo] = _OoXX
        else
            _oloX.error("service unavailable: %s", _oXxo)
        end
    end
    if _xolx.Players and not _xolx.Players.LocalPlayer then
        local _XoOl = _loIx.clock() + 10
        while not _xolx.Players.LocalPlayer and _loIx.clock() < _XoOl do task.wait(0.1) end
        if _xolx.Players.LocalPlayer then
            _oloX._XIxo("LocalPlayer arrived late (%.1fs) - waited for it", 10 - (_XoOl - _loIx.clock()))
        else
            _oloX.error("Players.LocalPlayer is still nil after 10s")
        end
    end
    _xolx.LocalPlayer = _xolx.Players and _xolx.Players.LocalPlayer
    return _xolx
end)
_XIxX.module("core.net", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _oloX = _XIxX.require("boot.log").for_module("net")
    local _xolx = {}
    local _IIIl, _loO = nil, 0
    local _lx = 30
    local function networking()
        local _XooX = _loIx.clock()
        if _IIIl and _IIIl.Parent and (_XooX - _loO) < _lx then
            return _IIIl
        end
        local _xlIX = _OoXX.ReplicatedStorage:FindFirstChild("Packages")
        local _OooX = _xlIX and _xlIX:FindFirstChild("Networking")
        _IIIl, _loO = _OooX, _XooX
        return _OooX
    end
    function _xolx.find(_oXxo)
        local _OooX = networking()
        return _OooX and _OooX:FindFirstChild(_oXxo) or nil
    end
    function _xolx.call(_oXxo, ...)
        local _XxIx = _xolx.find(_oXxo)
        if not _XxIx then return false, "remote not found: " .. tostring(_oXxo) end
        local _xOIx, _oXlx, _XXlx = pcall(function(...) return _XxIx:InvokeServer(...) end, ...)
        if not _xOIx then return false, tostring(_oXlx) end
        return _oXlx, _XXlx
    end
    function _xolx.fire(_oXxo, ...)
        local _oxIx = _xolx.find(_oXxo)
        if not _oxIx then return false, "remote not found: " .. tostring(_oXxo) end
        local _xOIx, _loOX = pcall(function(...) _oxIx:FireServer(...) end, ...)
        if not _xOIx then return false, tostring(_loOX) end
        return true
    end
    return _xolx
end)
_XIxX.module("core.data", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _oOXo = _XIxX.require("core.exec")
    local _oloX  = _XIxX.require("boot.log").for_module("data")
    local _xolx = {}
    local _IxxO = {}      -- key -> { mod = <required value> } or { missing = true }
    local function atPath(...)
        local _Ixxo = _OoXX.ReplicatedStorage
        for _OXlx, _XIIX in ipairs({ ... }) do
            if not _Ixxo then return nil end
            _Ixxo = _Ixxo:FindFirstChild(_XIIX)
        end
        return _Ixxo
    end
    local function searchModule(_oXxo)
        for _OXlx, _Ixlx in ipairs(_OoXX.ReplicatedStorage:GetDescendants()) do
            if _Ixlx:IsA("ModuleScript") and _Ixlx.Name == _oXxo then return _Ixlx end
        end
        return nil
    end
    local function resolve(_xIoX, _IlIX)
        local _lxXo = _IxxO[_xIoX]
        if _lxXo then return _lxXo._XOoX end
        if not _oOXo.can.gameRequire then
            _oloX.error("cannot require game modules on this executor (%s) - %s unavailable",
                tostring(_oOXo.gameRequireWhy), _IlIX[#_IlIX])
            _IxxO[_xIoX] = { _OlIO = true }
            return nil
        end
        local _oXxo = _IlIX[#_IlIX]
        local _xIxo = atPath(table.unpack(_IlIX))
        if not (_xIxo and _xIxo:IsA("ModuleScript")) then
            _xIxo = searchModule(_oXxo)
            if _xIxo then
                _oloX.warn("%s was not at %s - found it at %s",
                    _oXxo, table.concat(_IlIX, "."), _xIxo:GetFullName())
            end
        end
        if not _xIxo then
            _IxxO[_xIoX] = { _OlIO = true }
            _oloX.error("could not resolve the game module %s (expected %s)",
                _oXxo, table.concat(_IlIX, "."))
            return nil
        end
        local _XOoX
        local _xOIx = _XIxX.try("data.require." .. _xIoX, function() _XOoX = require(_xIxo) end)
        if not _xOIx or type(_XOoX) ~= "table" then
            _IxxO[_xIoX] = { _OlIO = true }
            _oloX.error("%s could not be required", _xIxo:GetFullName())
            return nil
        end
        _IxxO[_xIoX] = { _XOoX = _XOoX }
        return _XOoX
    end
    function _xolx.assets()        return resolve("assets", { "Data", "Assets" }) end
    function _xolx._ooxO()         return resolve("areas", { "Data", "Areas" }) end
    function _xolx.eggState()      return resolve("eggState", { "Client", "EggState" }) end
    function _xolx.assetEarnings() return resolve("assetEarnings", { "Shared", "Util", "AssetEarnings" }) end
    function _xolx.plotState()     return resolve("plotState", { "Client", "PlotState" }) end
    function _xolx.slotIdentity()  return resolve("slotIdentity", { "Shared", "Util", "AreaEggSlotIdentity" }) end
    function _xolx.resetWall()     return resolve("resetWall", { "Client", "AreaEggResetWall" }) end
    function _xolx.bases()         return resolve("bases", { "Data", "Bases" }) end
    function _xolx._lxIX()          return resolve("save", { "Shared", "Save" }) end
    function _xolx.eggCycle()      return resolve("eggCycle", { "Shared", "Util", "AreaEggCycle" }) end
    function _xolx.fusionFlags()   return resolve("fusionFlags", { "Shared", "Flags", "ShrineFusionFlags" }) end
    local _oo = 115
    function _xolx.eggInventory()
        local _xIIo, _xIlo
        _XIxX.try("data.eggInventoryCount", function()
            local _lxIX = _xolx._lxIX()
            local _llOx = _lxIX and _lxIX.Get and _lxIX.Get(_OoXX.Players.LocalPlayer)
            if type(_llOx) == "table" and type(_llOx.EggInventory) == "table" then
                _xIIo = 0
                for _OXlx in pairs(_llOx.EggInventory) do _xIIo = _xIIo + 1 end
            end
        end)
        _XIxX.try("data.eggInventoryLimit", function()
            local _IoIo = _xolx.fusionFlags()
            local _Oxlx = _IoIo and _IoIo.EggInventoryLimit
            _xIlo = _Oxlx and type(_Oxlx.Get) == "function" and tonumber(_Oxlx:Get()) or nil
        end)
        _xIlo = _xIlo or _oo
        if not _xIIo then return nil, nil, _xIlo end
        return _xIIo >= _xIlo, _xIIo, _xIlo
    end
    function _xolx.secondsUntilReset()
        local _lOOX = _xolx.eggCycle()
        if not (_lOOX and type(_lOOX.SecondsUntilReset) == "function") then return nil end
        local _xOIx, _llOx = pcall(_lOOX.SecondsUntilReset, workspace:GetServerTimeNow())
        return _xOIx and tonumber(_llOx) or nil
    end
    function _xolx.fieldSealed()
        local _OolX = _xolx.resetWall()
        if not (_OolX and type(_OolX.IsSealed) == "function") then return nil end
        local _xOIx, _oOXO = pcall(_OolX.IsSealed)
        if not _xOIx then return nil end
        return _oOXO == true
    end
    function _xolx.assetsDir()
        local _oXlx = _xolx.assets()
        return _oXlx and _oXlx.Directory or nil
    end
    function _xolx.areasDir()
        local _oXlx = _xolx._ooxO()
        return _oXlx and _oXlx.Directory or nil
    end
    function _xolx.report()
        local _lxoX = {}
        for _xIoX, _lxXo in pairs(_IxxO) do
            _lxoX[#_lxoX + 1] = _xIoX .. (_lxXo._OlIO and "=MISSING" or "=ok")
        end
        table._lIlX(_lxoX)
        return _lxoX
    end
    return _xolx
end)
_XIxX.module("core.profiles", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _oOXo = _XIxX.require("core.exec")
    local _oloX  = _XIxX.require("boot.log").for_module("profiles")
    local _xolx = {}
    local _lxlO = 1
    local _XXlX = "RyuzakiHub/profiles"
    local _oIOl = "RyuzakiHub/settings.json"
    _xolx._lxlO = _lxlO
    local _xOx = { "url", "token", "secret", "key", "password" }
    local _IlxO = {
        AntiTreadmill  = true,   -- a preference, and it only stands down a belt
        FarmAreas      = true,   -- filter
        FarmRarities   = true,   -- filter
        FarmTargetBy   = true,   -- filter
        WebhookOn      = true,   -- the switch only; the URL carries no flag
        Theme          = true,   -- appearance
        Background     = true,   -- appearance (the asset id, never an object)
    }
    _xolx._IlxO = _IlxO
    local function _OllO(_oXxo)
        if not _IlxO[_oXxo] then return true end
        local _oIOx = tostring(_oXxo):lower()
        for _OXlx, bad in ipairs(_xOx) do
            if _oIOx:find(bad, 1, true) then return true end
        end
        return false
    end
    function _xolx.available()
        return _oOXo.can._oOIo and _oOXo.can.folders and true or false
    end
    local _llIO, _IxIl = {}, false
    local function safeName(_oXxo)
        _oXxo = tostring(_oXxo or ""):gsub("[^%w%-_ ]", ""):gsub("^%s+", ""):gsub("%s+$", "")
        return _oXxo
    end
    local function pathFor(_oXxo)
        return _XXlX .. "/" .. _oXxo .. ".json"
    end
    function _xolx._oxIO()
        _llIO, _IxIl = {}, false
        if not _xolx.available() then return _llIO end
        _XIxX.try("profiles.refresh", function()
            _oOXo.ensureFolder("RYUZAKI HUB")
            _oOXo.ensureFolder(_XXlX)
            local _oOIo = _oOXo.listFiles(_XXlX)
            if not _oOIo then
                _oloX.warn("this executor has no listfiles - saved profiles cannot be listed")
                return
            end
            for _OXlx, _Oxlx in ipairs(_oOIo) do
                local _oXxo = tostring(_Oxlx):match("([^/\\]+)%.json$")
                if _oXxo then _llIO[#_llIO + 1] = _oXxo end
            end
            table._lIlX(_llIO)
            _IxIl = true
        end)
        return _llIO
    end
    function _xolx._OOxo()
        if not _IxIl then _xolx._oxIO() end
        return _llIO
    end
    local _xIX = nil
    function _xolx.setFlagSource(_xxxX) _xIX = _xxxX end
    local _Xl, _oO = nil, nil
    function _xolx.setAppearanceHooks(read, _OoxO)
        _Xl, _oO = read, _OoxO
    end
    local function collectFlags()
        local _lxoX = {}
        if type(_xIX) ~= "function" then return _lxoX end
        local _xOIx, _IoIo = pcall(_xIX)
        if not _xOIx or type(_IoIo) ~= "table" then return _lxoX end
        for _oXxo, _OxxX in pairs(_IoIo) do
            if not _OllO(_oXxo) then
                local _XlOx
                if type(_OxxX) == "table" then
                    _XlOx = _OxxX.CurrentValue
                    if _XlOx == nil then _XlOx = _OxxX.Value end
                    if _XlOx == nil then _XlOx = _OxxX._XxOo end
                else
                    _XlOx = _OxxX
                end
                local _OlOx = type(_XlOx)
                if _OlOx == "boolean" or _OlOx == "number" or _OlOx == "string" then
                    _lxoX[tostring(_oXxo)] = _XlOx
                elseif _OlOx == "table" then
                    local _OIXo = {}
                    for _xxlx, _Ilxo in ipairs(_XlOx) do
                        if type(_Ilxo) == "string" or type(_Ilxo) == "number" then
                            _OIXo[_xxlx] = _Ilxo
                        end
                    end
                    _lxoX[tostring(_oXxo)] = _OIXo
                end
            end
        end
        return _lxoX
    end
    function _xolx._lxIX(_oXxo)
        if not _xolx.available() then return false, "This executor cannot save files" end
        _oXxo = safeName(_oXxo)
        if _oXxo == "" then return false, "Give the profile a name" end
        local _loIO = {
            version = _lxlO,
            _OIOo = _loIx.date("!%Y-%m-%dT%H:%M:%SZ"),
            _XXxO = tostring(_XIxX._XXxO),
            _IoIo = collectFlags(),
            appearance = (type(_Xl) == "function")
                and select(2, pcall(_Xl)) or nil,
        }
        local _Ixoo
        local _OOlo = pcall(function() _Ixoo = _OoXX.HttpService:JSONEncode(_loIO) end)
        if not _OOlo or not _Ixoo then return false, "Could not encode the profile" end
        local _IlIX = pathFor(_oXxo)
        local _xOIx = _XIxX.try("profiles.save", function()
            _oOXo.ensureFolder("RYUZAKI HUB")
            _oOXo.ensureFolder(_XXlX)
            if not _oOXo.writeFile(_IlIX, _Ixoo) then error("writefile refused", 0) end
        end)
        if not _xOIx then return false, "Could not write the profile" end
        if not _oOXo.isFile(_IlIX) then
            _oloX.warn("profile %q: writefile returned but isfile says no", _oXxo)
            return false, "Written but not found - this executor's file access is broken"
        end
        local _oooo = _oOXo.readFile(_IlIX)
        if _oooo ~= _Ixoo then
            _oloX.warn("profile %q: readback mismatch (%d vs %d bytes)", _oXxo,
                type(_oooo) == "string" and #_oooo or -1, #_Ixoo)
            return false, "Written but readback differs - not saved"
        end
        _xolx._oxIO()
        _oloX._XIxo("saved profile %q (%d flags)", _oXxo, (function()
            local _oIOx = 0 for _OXlx in pairs(_loIO._IoIo) do _oIOx = _oIOx + 1 end return _oIOx
        end)())
        return true, "Saved " .. _oXxo
    end
    function _xolx.load(_oXxo)
        if not _xolx.available() then return false, "This executor cannot read files" end
        _oXxo = safeName(_oXxo)
        if _oXxo == "" then return false, "Pick a profile" end
        local _IlIX = pathFor(_oXxo)
        if not _oOXo.isFile(_IlIX) then return false, "No profile called " .. _oXxo end
        local _Ixoo = _oOXo.readFile(_IlIX)
        if type(_Ixoo) ~= "string" or _Ixoo == "" then
            return false, _oXxo .. " is empty"
        end
        local _XIXo
        local _lOlo = pcall(function() _XIXo = _OoXX.HttpService:JSONDecode(_Ixoo) end)
        if not _lOlo or type(_XIXo) ~= "table" then
            _oloX.warn("profile %q is not valid JSON - refusing it", _oXxo)
            return false, _oXxo .. " is corrupt"
        end
        local _XlOx = tonumber(_XIXo.version) or 0
        if _XlOx > _lxlO then
            return false, _oXxo .. " was saved by a newer version"
        end
        if _XlOx < _lxlO then
            _oloX._XIxo("profile %q is format %d, current is %d - loading as-is", _oXxo, _XlOx, _lxlO)
        end
        local _lXXl = 0
        if type(_XIXo._IoIo) == "table" and type(_xIX) == "function" then
            local _xOIx, _IoIo = pcall(_xIX)
            if _xOIx and type(_IoIo) == "table" then
                for _xIoX, _XxOo in pairs(_XIXo._IoIo) do
                    local _OxxX = (not _OllO(_xIoX)) and _IoIo[_xIoX] or nil
                    if type(_OxxX) == "table" and type(_OxxX.Set) == "function" then
                        if _XIxX.try("profiles.set." .. tostring(_xIoX), function()
                            _OxxX:Set(_XxOo)
                        end) then
                            _lXXl = _lXXl + 1
                        end
                    end
                end
            end
        end
        if type(_XIXo.appearance) == "table" and type(_oO) == "function" then
            _XIxX.try("profiles.appearance", function() _oO(_XIXo.appearance) end)
        end
        _oloX._XIxo("loaded profile %q (%d controls)", _oXxo, _lXXl)
        return true, ("Loaded %s (%d settings)"):format(_oXxo, _lXXl)
    end
    function _xolx.delete(_oXxo)
        if not _xolx.available() then return false, "This executor cannot delete files" end
        _oXxo = safeName(_oXxo)
        local _IlIX = pathFor(_oXxo)
        if _oXxo == "" or not _oOXo.isFile(_IlIX) then return false, "No such profile" end
        local _xOIx = _XIxX.try("profiles.delete", function() _oOXo.deleteFile(_IlIX) end)
        _xolx._oxIO()
        if not _xOIx then return false, "Could not delete " .. _oXxo end
        _oloX._XIxo("deleted profile %q", _oXxo)
        return true, "Deleted " .. _oXxo
    end
    local function readSettings()
        if not _xolx.available() or not _oOXo.isFile(_oIOl) then return {} end
        local _Ixoo = _oOXo.readFile(_oIOl)
        local _XIXo
        pcall(function() _XIXo = _OoXX.HttpService:JSONDecode(_Ixoo) end)
        return type(_XIXo) == "table" and _XIXo or {}
    end
    function _xolx.autoLoadName()
        local _llOx = readSettings()
        local _oIOx = _llOx.autoLoad
        return type(_oIOx) == "string" and _oIOx ~= "" and _oIOx or nil
    end
    function _xolx.setAutoLoad(_oXxo)
        if not _xolx.available() then return false, "This executor cannot save files" end
        _oXxo = safeName(_oXxo)
        local _llOx = readSettings()
        _llOx.autoLoad = (_oXxo ~= "" and _oXxo) or nil
        _llOx.version = _lxlO
        local _Ixoo
        if not pcall(function() _Ixoo = _OoXX.HttpService:JSONEncode(_llOx) end) then
            return false, "Could not save the setting"
        end
        _XIxX.try("profiles.settings", function()
            _oOXo.ensureFolder("RYUZAKI HUB")
            _oOXo.writeFile(_oIOl, _Ixoo)
        end)
        _oloX._XIxo("auto-load profile is now %s", _oXxo ~= "" and ("%q"):format(_oXxo) or "off")
        return true, _oXxo ~= "" and ("Auto-loading " .. _oXxo) or "Auto-load off"
    end
    local _oOO = false
    function _xolx.runAutoLoad()
        if _oOO then return false, "already ran" end
        _oOO = true
        local _oXxo = _xolx.autoLoadName()
        if not _oXxo then return false, "no auto-load profile set" end
        local _xOIx, _IooX = _xolx.load(_oXxo)
        if not _xOIx then _oloX.warn("auto-load failed: %s", tostring(_IooX)) end
        return _xOIx, _IooX
    end
    return _xolx
end)
_XIxX.module("core.exec", function(_XIxX)
    local _oloX = _XIxX.require("boot.log").for_module("exec")
    local _xolx = {}
    local _IoOX = (type(getgenv) == "function" and getgenv()) or _G
    local _IlXo = type(_IoOX.RYUZAKI_CAPS_DENY) == "table" and _IoOX.RYUZAKI_CAPS_DENY or {}
    _xolx.simulatedDenies = _IlXo
    local function _xxxX(_oXxo)
        if _IlXo[_oXxo] then return nil end
        local _xOIx, _XlOx
        _xOIx, _XlOx = pcall(function() return type(getgenv) == "function" and getgenv()[_oXxo] or nil end)
        if not _xOIx or type(_XlOx) ~= "function" then
            _xOIx, _XlOx = pcall(function() return getfenv and getfenv()[_oXxo] or nil end)
        end
        if not _xOIx or type(_XlOx) ~= "function" then
            _xOIx, _XlOx = pcall(function() return (_G and _G[_oXxo]) end)
        end
        if not _xOIx or type(_XlOx) ~= "function" then
            _xOIx, _XlOx = pcall(function()
                local _xxxO = loadstring and loadstring("return " .. _oXxo)
                return _xxxO and _xxxO() or nil
            end)
        end
        return (_xOIx and type(_XlOx) == "function") and _XlOx or nil
    end
    local function _xOIo(...)
        for _OXlx, _oXxo in ipairs({ ... }) do
            local _Oxlx = _xxxX(_oXxo)
            if _Oxlx then return _Oxlx, _oXxo end
        end
        return nil, nil
    end
    local _OXO   = _xOIo("writefile")
    local _oIX    = _xOIo("readfile")
    local _oxOl      = _xOIo("isfile")
    local _xIIl     = _xOIo("delfile")
    local _OIX    = _xOIo("isfolder")
    local _XXl  = _xOIo("makefolder")
    local _IXO   = _xOIo("listfiles")
    local _lIl = _xOIo("getcustomasset", "getsynasset")
    local _lxOl      = _xOIo("gethui")
    local _IOxl       = _xOIo("getgc")
    local _IIX    = _xOIo("getconnections")
    local _OxOl      = _xOIo("hookfunction", "replaceclosure")
    local _oXl  = _xOIo("getrawmetatable")
    local _OIl = _xOIo("setreadonly", "make_writeable")
    local _lXO   = _xOIo("queue_on_teleport", "queueonteleport")
    local _lIX    = _xOIo("identifyexecutor", "getexecutorname")
    local _OXl  = _xOIo("fireproximityprompt")
    local _OxOO, _ooOl = _xOIo("setclipboard", "toclipboard", "set_clipboard", "setrbxclipboard")
    local _Oxo, _IxX = false, "no ModuleScript to probe"
    do
        local _xOIx, _loOX = pcall(function()
            local _OlxX = game:GetService("ReplicatedStorage")
            local _lxlo = _OlxX:FindFirstChildWhichIsA("ModuleScript", true)
            if not _lxlo then return end
            local _IlOx = require(_lxlo)
            _Oxo, _IxX = true, _lxlo:GetFullName()
        end)
        if not _xOIx then _IxX = tostring(_loOX) end
        if _IlXo.gameRequire then _Oxo, _IxX = false, "simulated deny" end
    end
    local _IlIl, _Ilo
    do
        local _xOIx, _XlOx = pcall(function() return syn and syn._xxIO end)
        if _xOIx and type(_XlOx) == "function" then
            _IlIl, _Ilo = _XlOx, "syn.request"
        else
            _xOIx, _XlOx = pcall(function() return http and http._xxIO end)
            if _xOIx and type(_XlOx) == "function" then
                _IlIl, _Ilo = _XlOx, "http.request"
            else
                _IlIl, _Ilo = _xOIo("request", "http_request", "httprequest")
            end
        end
    end
    _xolx.can = {
        _oOIo      = (_OXO and _oIX and _oxOl) and true or false,
        folders    = (_OIX and _XXl) and true or false,
        listFiles  = _IXO and true or false,
        customAsset = _lIl and true or false,
        hiddenUi   = _lxOl and true or false,
        gc         = _IOxl and true or false,
        connections = _IIX and true or false,
        hooking    = (_OxOl and _oXl) and true or false,
        clipboard  = _OxOO and true or false,
        _xxIO    = _IlIl and true or false,
        teleportQueue = _lXO and true or false,
        _xXIO    = true,
        gameRequire = _Oxo,
    }
    _xolx.promptVia = _OXl and "fireproximityprompt" or "InputHoldBegin"
    _xolx.gameRequireWhy = _IxX
    _xolx._oXxo = "unknown"
    if _lIX then
        local _xOIx, _oIOx = pcall(_lIX)
        if _xOIx and type(_oIOx) == "string" and #_oIOx > 0 then _xolx._oXxo = _oIOx end
    end
    function _xolx.hiddenParent()
        if _lxOl then
            local _xOIx, _xllx = pcall(_lxOl)
            if _xOIx and _xllx then return _xllx end
        end
        return _XIxX.require("core.services").CoreGui
    end
    function _xolx.writeFile(_IlIX, _XIXo)
        if not _OXO then return false end
        return (_XIxX.try("exec.writeFile", _OXO, _IlIX, _XIXo))
    end
    function _xolx.readFile(_IlIX)
        if not _oIX then return nil end
        local _xOIx, _XIXo = _XIxX.try("exec.readFile", _oIX, _IlIX)
        return _xOIx and _XIXo or nil
    end
    function _xolx.isFile(_IlIX)
        if not _oxOl then return false end
        local _xOIx, _lIxX = pcall(_oxOl, _IlIX)
        return _xOIx and _lIxX or false
    end
    function _xolx.listFiles(_IlIX)
        if not _IXO then return nil end
        local _xOIx, _oOIo = _XIxX.try("exec.listFiles", _IXO, _IlIX)
        if not _xOIx or type(_oOIo) ~= "table" then return nil end
        return _oOIo
    end
    function _xolx.deleteFile(_IlIX)
        if not _xIIl then return false end
        return (_XIxX.try("exec.deleteFile", _xIIl, _IlIX))
    end
    function _xolx.ensureFolder(_IlIX)
        if not _xolx.can.folders then return false end
        local _xXxO = ""
        for _XIIX in tostring(_IlIX):gmatch("[^/]+") do
            _xXxO = (_xXxO == "") and _XIIX or (_xXxO .. "/" .. _XIIX)
            local _xOIx, _IxOO = pcall(_OIX, _xXxO)
            if _xOIx and not _IxOO then
                if not _XIxX.try("exec.makeFolder", _XXl, _xXxO) then return false end
            end
        end
        return true
    end
    function _xolx.customAsset(_IlIX)
        if not _lIl then return nil end
        local _xOIx, _OlIx = _XIxX.try("exec.customAsset", _lIl, _IlIX)
        return _xOIx and _OlIx or nil
    end
    function _xolx.clipboard(_OllX)
        for _OXlx, _oXxo in ipairs({ "setclipboard", "toclipboard", "set_clipboard", "setrbxclipboard" }) do
            local _Oxlx = _xxxX(_oXxo)
            if _Oxlx and pcall(_Oxlx, _OllX) then return true end
        end
        return false
    end
    function _xolx.httpRequest(_Xxxo)
        if not _IlIl then return nil end
        local _xOIx, _OlXX = _XIxX.try("exec.httpRequest", _IlIl, _Xxxo)
        return _xOIx and _OlXX or nil
    end
    function _xolx.gcScan(tablesOnly)
        if not _IOxl then return {} end
        local _Ollx = _loIx.clock()
        local _xOIx, _Oxxo = _XIxX.try("exec.gcScan", _IOxl, tablesOnly and true or false)
        if not _xOIx or type(_Oxxo) ~= "table" then return {} end
        local _oOIx = (_loIx.clock() - _Ollx) * 1000
        _xolx.lastGcMs = _oOIx
        _oloX.warn("gc sweep: %d objects in %.0fms", #_Oxxo, _oOIx)
        return _Oxxo
    end
    function _xolx.firePrompt(prompt, holdDuration)
        if _OXl then
            return (_XIxX.try("exec.firePrompt", _OXl, prompt, holdDuration or 0))
        end
        return (_XIxX.try("exec.firePrompt.hold", function()
            prompt:InputHoldBegin()
            local _oxXo = tonumber(holdDuration)
            if _oxXo == nil then _oxXo = tonumber(prompt.HoldDuration) or 0 end
            if _oxXo > 0 then task.wait(_oxXo + 0.05) end
            prompt:InputHoldEnd()
        end))
    end
    function _xolx.report()
        local _xXXo, _OlIO = {}, {}
        for _IIOx, _XlOx in pairs(_xolx.can) do
            table.insert(_XlOx and _xXXo or _OlIO, _IIOx)
        end
        table._lIlX(_xXXo); table._lIlX(_OlIO)
        local _oXOO = {}
        for _IIOx in pairs(_IlXo) do _oXOO[#_oXOO + 1] = tostring(_IIOx) end
        table._lIlX(_oXOO)
        return {
            executor = _xolx._oXxo,
            _xXXo = _xXXo,
            _OlIO = _OlIO,
            _oXOO = _oXOO,
            promptVia = _xolx.promptVia,
            gameRequireWhy = _IxX,
        }
    end
    local _IlOx = _xolx.report()
    _oloX._XIxo("executor=%s clipboard=%s request=%s prompts=%s gameRequire=%s (%s)",
        _xolx._oXxo, tostring(_ooOl), tostring(_Ilo), _xolx.promptVia,
        tostring(_Oxo), tostring(_IxX))
    if #_IlOx._oXOO > 0 then
        _oloX.warn("SIMULATED capability denies active: %s", table.concat(_IlOx._oXOO, ", "))
    end
    _oloX._XIxo("supported: %s", #_IlOx._xXXo > 0 and table.concat(_IlOx._xXXo, ", ") or "(none)")
    if #_IlOx._OlIO > 0 then
        _oloX.warn("unsupported here: %s", table.concat(_IlOx._OlIO, ", "))
    end
    return _xolx
end)
_XIxX.module("core.device", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _XlOX = _XIxX.require("core.config")
    local _oloX = _XIxX.require("boot.log").for_module("device")
    local _xolx = {}
    _xolx.isTouch = _OoXX.UserInputService.TouchEnabled
        and not _OoXX.UserInputService.KeyboardEnabled
    local function shortSide()
        local _llOX = workspace.CurrentCamera
        local _lOlx = _llOX and _llOX.ViewportSize
        if not _lOlx or _lOlx.Y < 10 then return 1080 end
        return math.min(_lOlx.X, _lOlx.Y)
    end
    _xolx.smallScreen = shortSide() < 500
    _xolx.tier = (_xolx.isTouch and _xolx.smallScreen) and "low" or "mid"
    _xolx._IXOX = nil
    local _Oloo = { _XloX = 2.2, _oOoX = 1.35, high = 1.0 }
    function _xolx._oIOo(_xIlO)
        return _xIlO * (_Oloo[_xolx.tier] or 1.35)
    end
    function _xolx._OOOO(_oIOx)
        local _xIOo = (_xolx.tier == "low" and 0.35) or (_xolx.tier == "mid" and 0.7) or 1
        return math._IOoX(1, math.floor(_oIOx * _xIOo + 0.5))
    end
    function _xolx.lite()
        return _xolx.tier == "low"
    end
    local _xXIl = {}
    function _xolx.onTier(_lIlx, _xxIo, _xxxX)
        _xXIl[#_xXIl + 1] = { scope = _lIlx, _xxIo = _xxIo, _xxxX = _xxxX }
    end
    local function setTier(_OlOx)
        if _xolx.tier == _OlOx then return end
        local _lxXX = _xolx.tier
        _xolx.tier = _OlOx
        _oloX._XIxo("tier %s -> %s (fps %.0f, touch=%s, short=%d)",
            _lxXX, _OlOx, _xolx._IXOX or -1, tostring(_xolx.isTouch), shortSide())
        for _xxlx = #_xXIl, 1, -1 do
            local _Xolx = _xXIl[_xxlx]
            if not _Xolx.scope or _Xolx.scope._xIXo then
                table.remove(_xXIl, _xxlx)
            else
                _XIxX.try("device/" .. _Xolx._xxIo, _Xolx._xxxX, _OlOx, _lxXX)
            end
        end
    end
    local _lIlx = _XIxX.scope("core.device")
    local _XoIl, _oOoO = _XIxX._XXIO.frameNo, _loIx.clock()
    local _OoIO, _oxl = nil, 0
    _lIlx:loop("measure", 5, function()
        local _XooX = _loIx.clock()
        local _IXOX = (_XIxX._XXIO.frameNo - _XoIl) / math._IOoX(_XooX - _oOoO, 0.001)
        _XoIl, _oOoO = _XIxX._XXIO.frameNo, _XooX
        _xolx._IXOX = _xolx._IXOX and (_xolx._IXOX + (_IXOX - _xolx._IXOX) * 0.4) or _IXOX
        local _oolX = _xolx.tier
        if _xolx.tier == "high" then
            if _xolx._IXOX < 45 then _oolX = "mid" end
        elseif _xolx.tier == "mid" then
            if _xolx._IXOX < _XlOX.LITE_FPS then _oolX = "low"
            elseif _xolx._IXOX > 75 then _oolX = "high" end
        else
            if _xolx._IXOX > 40 then _oolX = "mid" end
        end
        if _oolX == "high" and _xolx.isTouch and _xolx.smallScreen then _oolX = "mid" end
        if _oolX == _xolx.tier then
            _OoIO, _oxl = nil, 0
            return
        end
        if _OoIO == _oolX then
            _oxl = _oxl + 1
        else
            _OoIO, _oxl = _oolX, 1
        end
        if _oxl >= 2 then
            setTier(_oolX)
            _OoIO, _oxl = nil, 0
        end
    end)
    _oloX._XIxo("start tier=%s touch=%s smallScreen=%s", _xolx.tier,
        tostring(_xolx.isTouch), tostring(_xolx.smallScreen))
    return _xolx
end)
_XIxX.module("core.character", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _oloX = _XIxX.require("boot.log").for_module("character")
    local _xolx = {}
    local _oxoX = _OoXX.LocalPlayer
    local _oIxl = setmetatable({}, { __mode = "v" })
    local _xXIl = {}   -- { scope = sc, label = str, fn = fn }
    function _xolx.get()
        local _xXlx = _oIxl._xxoo
        if _xXlx and _xXlx.Parent then return _xXlx end
        return _oxoX and _oxoX.Character
    end
    function _xolx._oXIX()
        local _xXlx = _xolx.get()
        return _xXlx and _xXlx:FindFirstChild("HumanoidRootPart")
    end
    function _xolx.humanoid()
        local _xXlx = _xolx.get()
        return _xXlx and _xXlx:FindFirstChildOfClass("Humanoid")
    end
    local function fire(_xxoo)
        _oIxl._xxoo = _xxoo
        for _xxlx = #_xXIl, 1, -1 do
            local _Xolx = _xXIl[_xxlx]
            if not _Xolx.scope or _Xolx.scope._xIXo then
                table.remove(_xXIl, _xxlx)
            else
                _XIxX.try(("character/%s"):format(_Xolx._xxIo), _Xolx._xxxX, _xxoo)
            end
        end
    end
    function _xolx.onSpawn(_lIlx, _xxIo, _xxxX)
        _xXIl[#_xXIl + 1] = { scope = _lIlx, _xxIo = _xxIo, _xxxX = _xxxX }
        local _xXlx = _xolx.get()
        if _xXlx then _XIxX.try(("character/%s"):format(_xxIo), _xxxX, _xXlx) end
    end
    local _lIlx = _XIxX.scope("core.character")
    if _oxoX then
        _lIlx:connect(_oxoX.CharacterAdded, function(_xxoo)
            _oloX.trace("respawn")
            task.spawn(function()
                _XIxX.try("character/wait", function()
                    _xxoo:WaitForChild("HumanoidRootPart", 10)
                end)
                if _XIxX.alive() then fire(_xxoo) end
            end)
        end)
        _lIlx:connect(_oxoX.CharacterRemoving, function()
            _oIxl._xxoo = nil
        end)
        _oIxl._xxoo = _oxoX.Character
    else
        _oloX.error("no LocalPlayer - character tracking unavailable")
    end
    _xolx._listenerCount = function() return #_xXIl end
    return _xolx
end)
_XIxX.module("core.restore", function(_XIxX)
    local _lXxX  = _XIxX.require("core.character")
    local _oloX = _XIxX.require("boot.log").for_module("restore")
    local _xolx = {}
    local _Xlxl = {}     -- key -> { read, write, original, char, at }
    local _Oolo = {}       -- keys, in the order they were first captured
    _XIxX._XXIO._lIoo("restore.pending", function() return #_Oolo end)
    function _xolx.remember(_xIoX, read, write)
        if _Xlxl[_xIoX] then return false end
        local _xOIx, _XxOo = pcall(read)
        if not _xOIx then
            _oloX.warn("could not read %s to remember it: %s", _xIoX, tostring(_XxOo))
            return false
        end
        _Xlxl[_xIoX] = {
            read = read, write = write, original = _XxOo,
            _xxoo = _lXxX.get(), _oOxX = _loIx.clock(),
        }
        _Oolo[#_Oolo + 1] = _xIoX
        return true
    end
    function _xolx.onRestore(_xIoX, undo)
        if _Xlxl[_xIoX] then return false end
        _Xlxl[_xIoX] = { undo = undo, _xxoo = _lXxX.get(), _oOxX = _loIx.clock() }
        _Oolo[#_Oolo + 1] = _xIoX
        return true
    end
    function _xolx.permanent(_xIoX, _oxXX)
        if _Xlxl[_xIoX] then return false end
        _Xlxl[_xIoX] = { permanent = _oxXX or "not reversible", _xxoo = _lXxX.get() }
        _Oolo[#_Oolo + 1] = _xIoX
        return true
    end
    function _xolx.restoreAll()
        local _Ixol, _OllO, _oxOO = 0, 0, 0
        local _XOol = _lXxX.get()
        for _xxlx = #_Oolo, 1, -1 do
            local _xIoX = _Oolo[_xxlx]
            local _lxlx = _Xlxl[_xIoX]
            if _lxlx then
                if _lxlx.permanent then
                    _OllO = _OllO + 1
                elseif _lxlx._xxoo and _lxlx._xxoo ~= _XOol then
                    _OllO = _OllO + 1
                else
                    local _xOIx, _loOX = pcall(function()
                        if _lxlx.undo then _lxlx.undo() else _lxlx.write(_lxlx.original) end
                    end)
                    if _xOIx then
                        _Ixol = _Ixol + 1
                    else
                        _oxOO = _oxOO + 1
                        _oloX.error("restoring %s failed: %s", _xIoX, tostring(_loOX))
                    end
                end
                _Xlxl[_xIoX] = nil
            end
            table.remove(_Oolo, _xxlx)
        end
        return _Ixol, _OllO, _oxOO
    end
    function _xolx.audit()
        local _olIo = {}
        for _OXlx, _xIoX in ipairs(_Oolo) do
            local _lxlx = _Xlxl[_xIoX]
            if _lxlx and _lxlx.read then
                local _xOIx, _XooX = pcall(_lxlx.read)
                if _xOIx and tostring(_XooX) ~= tostring(_lxlx.original) then
                    _olIo[#_olIo + 1] = ("%s: %s (was %s)")
                        :format(_xIoX, tostring(_XooX), tostring(_lxlx.original))
                end
            elseif _lxlx and _lxlx.permanent then
                _olIo[#_olIo + 1] = ("%s: %s"):format(_xIoX, _lxlx.permanent)
            end
        end
        return _olIo
    end
    function _xolx._OoIO()
        return #_Oolo
    end
    local _lIlx = _XIxX.scope("core.restore")
    _lXxX.onSpawn(_lIlx, "restore.respawn", function(_xxoo)
        local _llxl = 0
        for _xxlx = #_Oolo, 1, -1 do
            local _xIoX = _Oolo[_xxlx]
            local _lxlx = _Xlxl[_xIoX]
            if _lxlx and _lxlx._xxoo and _lxlx._xxoo ~= _xxoo then
                _Xlxl[_xIoX] = nil
                table.remove(_Oolo, _xxlx)
                _llxl = _llxl + 1
            end
        end
        if _llxl > 0 then
            _oloX.trace("dropped %d entries captured against the old character", _llxl)
        end
    end)
    return _xolx
end)
_XIxX.module("core.config", function(_XIxX)
    return {
        CARRY_SPEED        = 500,
        OUTBOUND_SPEED_MIN = 500,
        OUTBOUND_SPEED_MAX = 1200,
        LITE_FPS           = 25,
        STATS_HZ           = 4,
        LOG_LEVEL          = 2,
        KEY_VALIDATE_URL   = "https://YOUR-VERCEL-URL/api/key/validate",
        KEY_SESSION_URL    = "",
        KEY_WEBSITE_URL    = "https://YOUR-VERCEL-URL/key.html",
        DEFAULT_BACKGROUND = "108858454360177",
    }
end)
_XIxX.module("core.state", function(_XIxX)
    return {
        heldEggUid   = nil,    -- written by: features.autosteal
        autoStealOn  = false,  -- written by: ui.window toggle
        stayOnTreadmill = false,
        lastFps      = 0,      -- written by: ui.stats
        _loll    = _loIx.clock(),
    }
end)
_XIxX.module("core.motion", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _oloX = _XIxX.require("boot.log").for_module("motion")
    local _xolx = {}
    local _IIOl = { autosteal = 100, bossfight = 90, _oxXo = 80, _ooOX = 50, _olOo = 40 }
    _xolx._IIOl = _IIOl
    local _ooOO = {}          -- owner -> true
    local _ooX = {}      -- owner -> fn(byOwner)
    local _xOOo = { _ooOO = 0, preempts = 0, _xXX = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx._Xolo()
        local _oXoo, _OXxO = nil, -1
        for _oXxo in pairs(_ooOO) do
            local _xIOx = _IIOl[_oXxo] or 0
            if _xIOx > _OXxO then _oXoo, _OXxO = _oXxo, _xIOx end
        end
        return _oXoo
    end
    function _xolx._XXx(_oXxo)
        local _Ooxo = _IIOl[_oXxo] or 0
        local _IXXX = _xolx._Xolo()
        if _IXXX and _IXXX ~= _oXxo and (_IIOl[_IXXX] or 0) > _Ooxo then return _IXXX end
        return nil
    end
    function _xolx.onPreempt(_oXxo, _xxxX) _ooX[_oXxo] = _xxxX end
    function _xolx.claim(_oXxo)
        local _XxXl = _xolx._XXx(_oXxo)
        if _ooOO[_oXxo] then return _XxXl == nil, _XxXl end
        _ooOO[_oXxo] = true
        _xOOo._ooOO = _xOOo._ooOO + 1
        local _Ooxo = _IIOl[_oXxo] or 0
        for other in pairs(_ooOO) do
            if other ~= _oXxo and (_IIOl[other] or 0) < _Ooxo and _ooX[other] then
                _xOOo.preempts = _xOOo.preempts + 1
                _XIxX.try("motion.preempt." .. other, _ooX[other], _oXxo)
            end
        end
        if _XxXl then _oloX._XIxo("%s claimed under %s (waiting)", _oXxo, _XxXl) end
        return _XxXl == nil, _XxXl
    end
    function _xolx.release(_oXxo)
        _ooOO[_oXxo] = nil
    end
    function _xolx.holds(_oXxo) return _ooOO[_oXxo] == true end
    local _xXX = {}      -- ring of { at, kind, owner }
    local _xloo = 64
    local _IxXo = 0
    local _xXIl = {}       -- { scope, fn }
    local function hasRelocate(_XlOx, _OlIo)
        _OlIo = _OlIo or 0
        if type(_XlOx) == "string" then return _XlOx:find("Relocate", 1, true) ~= nil end
        if type(_XlOx) == "table" and _OlIo < 2 then
            for _IIOx, _IOOx in pairs(_XlOx) do
                if hasRelocate(_IIOx, _OlIo + 1) or hasRelocate(_IOOx, _OlIo + 1) then return true end
            end
        end
        return false
    end
    local function reject(_Xlxo)
        _xOOo._xXX = _xOOo._xXX + 1
        _IxXo = (_IxXo % _xloo) + 1
        local _XooX = _loIx.clock()
        local _OxXX = _xolx._Xolo()
        _xXX[_IxXo] = { _oOxX = _XooX, _Xlxo = _Xlxo, _Xolo = _OxXX }
        _oloX._XIxo("server correction (%s) while %s owned the character", _Xlxo, tostring(_OxXX or "nobody"))
        for _xxlx = #_xXIl, 1, -1 do
            local _Xolx = _xXIl[_xxlx]
            if _Xolx.scope and _Xolx.scope._xIXo then
                table.remove(_xXIl, _xxlx)
            else
                _XIxX.try("motion.onRejected", _Xolx._xxxX, _Xlxo, _OxXX)
            end
        end
    end
    function _xolx.rejectionsSince(_OlOx)
        local _oIOx = 0
        for _OXlx, _IlOx in pairs(_xXX) do
            if _IlOx._oOxX >= (_OlOx or 0) then _oIOx = _oIOx + 1 end
        end
        return _oIOx
    end
    function _xolx.lastRejectionAt()
        local _xlxo = 0
        for _OXlx, _IlOx in pairs(_xXX) do if _IlOx._oOxX > _xlxo then _xlxo = _IlOx._oOxX end end
        return _xlxo
    end
    function _xolx.onRejected(scope, _xxxX)
        _xXIl[#_xXIl + 1] = { scope = scope, _xxxX = _xxxX }
    end
    local _lIlx = _XIxX.scope("core.motion")
    _XIxX.try("motion.watch", function()
        local _OooX = _OoXX.ReplicatedStorage:FindFirstChild("Packages")
        _OooX = _OooX and _OooX:FindFirstChild("Networking")
        if not _OooX then _oloX.warn("no Networking folder - corrections not observable") return end
        local _xoxO = _OooX:FindFirstChild("RE/RigSync/CorrectionBegan")
        if _xoxO and _xoxO:IsA("RemoteEvent") then
            _lIlx:connect(_xoxO.OnClientEvent, function() reject("CorrectionBegan") end)
        end
        local _oxIO = _OooX:FindFirstChild("RE/RigSync/Refresh")
        if _oxIO and _oxIO:IsA("RemoteEvent") then
            _lIlx:connect(_oxIO.OnClientEvent, function(...)
                for _xxlx = 1, select("#", ...) do
                    if hasRelocate((select(_xxlx, ...))) then reject("Relocate") return end
                end
            end)
        end
        _oloX._XIxo("watching RigSync corrections (began=%s refresh=%s)",
            tostring(_xoxO ~= nil), tostring(_oxIO ~= nil))
    end)
    _XIxX._XXIO._lIoo("motion.owner", function() return _xolx._Xolo() or "-" end)
    return _xolx
end)
_XIxX.module("core.util", function(_XIxX)
    local _xolx = {}
    function _xolx.clamp(_XlOx, lo, hi)
        return math._IOoX(lo, math.min(hi, _XlOx))
    end
    function _xolx.round(_XlOx, places)
        local _OIOx = 10 ^ (places or 0)
        return math.floor(_XlOx * _OIOx + 0.5) / _OIOx
    end
    function _xolx.wait(_xIlO)
        task.wait(_xIlO)
        return _XIxX.alive()
    end
    function _xolx._IlOo(_oIOx)
        if _oIOx >= 1e6 then return ("%.1fM"):format(_oIOx / 1e6) end
        if _oIOx >= 1e3 then return ("%.1fk"):format(_oIOx / 1e3) end
        return tostring(math.floor(_oIOx))
    end
    return _xolx
end)
_XIxX.module("ui.splash", function(_XIxX)
    -- Startup splash disabled: keep the hub from showing a loading/Discord overlay.
    local _xolx = {}
    _xolx._oIlX       = function() end
    _xolx.discord    = function() end
    _xolx.fail       = function() end
    _xolx._IOXo       = function() end
    _xolx.whenClosed = function(_xxxX) pcall(_xxxX) end
    _xolx.isWaitingForUser = function() return false end
    return _xolx
end)
_XIxX.module("ui.stats", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _XlOX = _XIxX.require("core.config")
    local _xIlx  = _XIxX.require("core.state")
    local _oloX = _XIxX.require("boot.log").for_module("stats")
    local _xolx = {}
    local _IOxO, RunService = _OoXX._IOxO, _OoXX.RunService
    local _oxlX, _olxX, _IlxX       = _OoXX.UserInputService, _OoXX.TweenService, _OoXX.HttpService
    local _lOO       = _OoXX._lOO
    local _IxlO  = Color3.fromRGB(26, 26, 30)
    local _xXlO  = Color3.fromRGB(14, 14, 17)
    local _XOXl = Color3.fromRGB(41, 41, 48)
    local _XXlO  = Color3.fromRGB(206, 206, 212)
    local _lloo    = Color3.fromRGB(240, 240, 246)
    local _lOoo    = Color3.fromRGB(220, 220, 220)
    local _OOoo    = Color3.fromRGB(240, 190, 90)
    local _OXlX     = Color3.fromRGB(240, 110, 110)
    local _Iloo, _Oox = Enum.Font.GothamMedium, 13
    local _XIOl = 0.45
    local _xxll = "RyuzakiHub_stats_pos.json"
    local _loo = 12     -- number glide, settles in ~0.25s
    local _oox  = 0.45   -- colour/icon cross-fade, seconds
    local _Xlx  = 0.28   -- lower = steadier, slower to react
    local _ooo = 0.30
    local _llxO = {
        _IXOX  = { _oOOX = -1,
                 warn = { enter = 50,  _XOXo = 54  },
                 bad  = { enter = 25,  _XOXo = 29  } },
        ping = { _oOOX = 1,
                 warn = { enter = 150, _XOXo = 132 },
                 bad  = { enter = 250, _XOXo = 220 } },
    }
    local _Iol  = 2.5   -- x the settled value counts as an outlier
    local _XlO   = 120   -- ms; below this, a jump is not worth doubting
    local _Xx = 2     -- consecutive samples before it is believed
    local _xlO = 6       -- seconds
    local _OlxO = "--"
    local _IOx = "RyuzakiHub/icons"
    local _Oxll  = _IOx .. "/v1"
    local _xlx = "https://raw.githubusercontent.com/google/material-design-icons/3.0.1/"
    local _oxll  = {
        clock = "action/2x_web/ic_schedule_white_48dp.png",
        pulse = "editor/2x_web/ic_show_chart_white_48dp.png",
        wifi  = "notification/2x_web/ic_wifi_white_48dp.png",
    }
    local _IoIl = {}   -- kind -> rbxasset:// once downloaded
    local _olol  = {}   -- kind -> colour currently applied
    local _XlX = false   -- fetched once per session, not per show()
    local _oOll = _loIx.clock()
    local _oXOX, _olIX, _IOXO, _OXXO
    local _lIlx   -- scope: created in build(), destroyed in teardown()
    local _IXoo, _lOoO, _XxOl, _loIl = {}, {}, {}, {}
    local _oxo = {}          -- kind -> the row Frame, for hover hit-testing
    local _xoXX, _xlXl, _IXll, _IOXl -- the hover/tap detail
    local _Olol = false
    local _lIoO, _lIXl = 0, nil
    local _oIol, _oIll = 0, 0
    local _XoIO, _lIo, _OoX = nil, 0, nil
    local _xOIl, _olX = nil, 0
    local _xXXO, _xooO, _lXOl = nil, false, false
    local _lOIl, _OOIl, _ooxl
    local _OXx, _lIxl = 1, false
    local function mk(_IIIo, _Oxlo, _xXoO)
        local _XIOx = Instance._oooX(_IIIo)
        for _IIOx, _XlOx in pairs(_Oxlo) do _XIOx[_IIOx] = _XlOx end
        _XIOx.Parent = _xXoO
        return _XIOx
    end
    local function tw(_XIOx, _OlOx, _Oxlo, _OoOo)
        _XIxX.try("stats.tween", function()
            _olxX:Create(_XIOx, TweenInfo._oooX(_OlOx, _OoOo or Enum.EasingStyle.Quint,
                Enum.EasingDirection.Out), _Oxlo):Play()
        end)
    end
    local function _lOxo(_xXoO, _XOlx, _Iolx, _xOlx, _lolx)
        local _IxxX, _lxxX = _xOlx - _XOlx, _lolx - _Iolx
        mk("Frame", {
            AnchorPoint = Vector2._oooX(0.5, 0.5),
            Position = UDim2.fromOffset((_XOlx + _xOlx) / 2, (_Iolx + _lolx) / 2),
            Size = UDim2.fromOffset(math.sqrt(_IxxX * _IxxX + _lxxX * _lxxX) + 1, 1.5),
            Rotation = math.deg(math.atan2(_lxxX, _IxxX)),
            BackgroundColor3 = _lloo, BorderSizePixel = 0,
        }, _xXoO)
    end
    local function drawIcon(_XIOX, _Xlxo)
        if _Xlxo == "clock" then
            local _OXIX = mk("Frame", {
                Position = UDim2.fromOffset(2, 2), Size = UDim2.fromOffset(12, 12),
                BackgroundTransparency = 1,
            }, _XIOX)
            mk("UICorner", { CornerRadius = UDim._oooX(0, 0) }, _OXIX)
            mk("UIStroke", { Color = _lloo, Thickness = 1.5 }, _OXIX)
            _lOxo(_XIOX, 8, 8, 8, 5)
            _lOxo(_XIOX, 8, 8, 10.5, 8)
        elseif _Xlxo == "pulse" then
            local _xIOx = { {1, 9}, {4.5, 9}, {6.5, 4}, {9.5, 13}, {11.5, 9}, {15, 9} }
            for _xxlx = 1, #_xIOx - 1 do _lOxo(_XIOX, _xIOx[_xxlx][1], _xIOx[_xxlx][2], _xIOx[_xxlx + 1][1], _xIOx[_xxlx + 1][2]) end
        else
            _IXoo = {}
            for _xxlx = 1, 3 do
                local _Xxlx = 2 + _xxlx * 3.5
                _IXoo[_xxlx] = mk("Frame", {
                    Position = UDim2.fromOffset(2 + (_xxlx - 1) * 4.5, 14 - _Xxlx),
                    Size = UDim2.fromOffset(3, _Xxlx),
                    BackgroundColor3 = _lloo, BorderSizePixel = 0,
                }, _XIOX)
                mk("UICorner", { CornerRadius = UDim._oooX(0, 0) }, _IXoo[_xxlx])
            end
        end
    end
    local function validPng(_XIXo)
        if type(_XIXo) ~= "string" or #_XIXo < 200 then return false end
        if _XIXo:_loXX(2, 4) ~= "PNG" then return false end
        local function be32(_oOxX)
            local _oXlx, _XXlx, _xXlx, _Ixlx = _XIXo:byte(_oOxX, _oOxX + 3)
            if not _Ixlx then return 0 end
            return ((_oXlx * 256 + _XXlx) * 256 + _xXlx) * 256 + _Ixlx
        end
        local _xlOx, _Xxlx = be32(17), be32(21)
        return _xlOx >= 16 and _xlOx <= 512 and _Xxlx >= 16 and _Xxlx <= 512
    end
    local function fillIcon(_XIOX, _Xlxo)
        for _OXlx, _xXlx in ipairs(_XIOX:GetChildren()) do _xXlx:Destroy() end
        if _Xlxo == "wifi" then _IXoo = {} end   -- the drawn bars just went away
        if _IoIl[_Xlxo] then
            mk("ImageLabel", {
                Name = "Img", Size = UDim2.fromScale(1, 1), BackgroundTransparency = 1,
                Image = _IoIl[_Xlxo], ImageColor3 = _olol[_Xlxo] or _lloo,
                ScaleType = Enum.ScaleType.Fit,
            }, _XIOX)
        else
            drawIcon(_XIOX, _Xlxo)
        end
    end
    local function _OIxo(_xXoO, _Xlxo)
        local _XIOX = mk("Frame", { Size = UDim2.fromOffset(16, 16), BackgroundTransparency = 1 }, _xXoO)
        _loIl[_Xlxo] = _XIOX
        fillIcon(_XIOX, _Xlxo)
        return _XIOX
    end
    local function cell(_xXoO, _Oolo, _Xlxo, _XIxO)
        local _xXlx = mk("Frame", {
            LayoutOrder = _Oolo, AutomaticSize = Enum.AutomaticSize.X,
            Size = UDim2.fromOffset(0, 18), BackgroundTransparency = 1,
        }, _xXoO)
        mk("UIListLayout", {
            FillDirection = Enum.FillDirection.Horizontal,
            VerticalAlignment = Enum.VerticalAlignment.Center,
            Padding = UDim._oooX(0, 6), SortOrder = Enum.SortOrder.LayoutOrder,
        }, _xXlx)
        _OIxo(_xXlx, _Xlxo).LayoutOrder = 1
        local _xlOx = 0
        _XIxX.try("stats.measure", function()
            _xlOx = _lOO:GetTextSize(_XIxO, _Oox, _Iloo, Vector2._oooX(1000, 100)).X
        end)
        return mk("TextLabel", {
            LayoutOrder = 2, AutomaticSize = Enum.AutomaticSize.X,
            Size = UDim2.fromOffset(math.ceil(_xlOx), 18), BackgroundTransparency = 1,
            Font = _Iloo, TextSize = _Oox, TextColor3 = _lOoo,
            TextXAlignment = Enum.TextXAlignment.Left, Text = "--",
        }, _xXlx)
    end
    local function divider(_xXoO, _Oolo)
        mk("Frame", {
            LayoutOrder = _Oolo, Size = UDim2.fromOffset(1, 14),
            BackgroundColor3 = _XXlO, BackgroundTransparency = 0.82,
            BorderSizePixel = 0, Name = "Divider",
        }, _xXoO)
    end
    local function clock(_llOx)
        _llOx = math.floor(_llOx)
        local _Xxlx, _OIOx = math.floor(_llOx / 3600), math.floor(_llOx / 60) % 60
        if _Xxlx > 0 then return ("%d:%02d:%02d"):format(_Xxlx, _OIOx, _llOx % 60) end
        return ("%02d:%02d"):format(_OIOx, _llOx % 60)
    end
    local function readPing()
        local _xOIx, _XlOx = pcall(function()
            return _IOxO.Network.ServerStatsItem["Data Ping"]:GetValue()
        end)
        if _xOIx and type(_XlOx) == "number" and _XlOx > 0 then return _XlOx end
        _xOIx, _XlOx = pcall(function() return _OoXX.LocalPlayer:GetNetworkPing() * 1000 end)
        return (_xOIx and type(_XlOx) == "number") and _XlOx or nil
    end
    local function paint(_IXoX, _xOIX, _oIIo)
        if _IXoX and _IXoX[_xOIX] ~= _oIIo then tw(_IXoX, _oox, { [_xOIX] = _oIIo }) end
    end
    local function ema(_oOIX, _XxOo, _IoxO)
        if _oOIX == nil then return _XxOo end
        return _oOIX + (_XxOo - _oOIX) * _IoxO
    end
    local _olO = { [0] = _lOoo, [1] = _OOoo, [2] = _OXlX }
    local function grade(_xooo, _XlOx, _IOOX)
        _IOOX = _IOOX or 0
        local function worseThan(_IOOx)
            if _xooo._oOOX < 0 then return _XlOx <= _IOOx else return _XlOx >= _IOOx end
        end
        local function betterThan(_IOOx)
            if _xooo._oOOX < 0 then return _XlOx >= _IOOx else return _XlOx <= _IOOx end
        end
        if _IOOX >= 2 then
            if not betterThan(_xooo.bad._XOXo) then return 2 end
            return betterThan(_xooo.warn._XOXo) and 0 or 1
        elseif _IOOX == 1 then
            if worseThan(_xooo.bad.enter) then return 2 end
            return betterThan(_xooo.warn._XOXo) and 0 or 1
        else
            if worseThan(_xooo.bad.enter) then return 2 end
            return worseThan(_xooo.warn.enter) and 1 or 0
        end
    end
    local _loXl = {
        _IXOX  = { [0] = "Smooth",    [1] = "Fair", [2] = "Poor" },
        ping = { [0] = "Excellent", [1] = "Good", [2] = "Poor" },
    }
    local function tintIcon(_Xlxo, _oIIo)
        if _olol[_Xlxo] == _oIIo then return end
        _olol[_Xlxo] = _oIIo
        local _XIOX = _loIl[_Xlxo]
        if not _XIOX or not _XIOX.Parent then return end
        for _OXlx, _Ixlx in ipairs(_XIOX:GetDescendants()) do
            if _Ixlx:IsA("ImageLabel") then
                paint(_Ixlx, "ImageColor3", _oIIo)
            elseif _Ixlx:IsA("UIStroke") then
                paint(_Ixlx, "Color", _oIIo)
            elseif _Ixlx:IsA("Frame") and _Ixlx.BackgroundTransparency < 1 then
                paint(_Ixlx, "BackgroundColor3", _oIIo)
            end
        end
    end
    local _IxlX = {
        { _xIoX = "fps",  _XoOX = "%d FPS" },
        { _xIoX = "ping", _XoOX = "%d ms"  },
    }
    local function entry(_xIoX)
        for _xxlx = 1, #_IxlX do
            if _IxlX[_xxlx]._xIoX == _xIoX then return _IxlX[_xxlx] end
        end
    end
    local function setTarget(_xIoX, _XxOo)
        local _lxlx = entry(_xIoX)
        if not _lxlx then return end
        _lxlx._xXXO = _XxOo
        if _lxlx._llOo == nil then _lxlx._llOo = _XxOo end
    end
    local function setUnavailable(_xIoX)
        local _lxlx = entry(_xIoX)
        if not _lxlx or _lxlx._xXXO == nil then return end
        _lxlx._llOo, _lxlx._xXXO, _lxlx.lastWhole = nil, nil, nil
        local _xxIo = _lOoO[_xIoX]
        if _xxIo and _xxIo.Text ~= _OlxO then _xxIo.Text = _OlxO end
    end
    local function easeNumbers(_xXxX)
        local _IIOx = 1 - math.exp(-_xXxX * _loo)
        for _xxlx = 1, #_IxlX do
            local _lxlx = _IxlX[_xxlx]
            local _xxIo = _lOoO[_lxlx._xIoX]
            if _lxlx._xXXO and _xxIo then
                local _XlXo = _lxlx._xXXO - _lxlx._llOo
                if _XlXo < 0.01 and _XlXo > -0.01 then
                    _lxlx._llOo = _lxlx._xXXO
                else
                    _lxlx._llOo += _XlXo * _IIOx
                end
                local _OIoo = math.floor(_lxlx._llOo + 0.5)
                if _OIoo ~= _lxlx.lastWhole then
                    _lxlx.lastWhole = _OIoo
                    _xxIo.Text = _lxlx._XoOX:format(_OIoo)
                end
            end
        end
    end
    local function resetNumbers()
        for _xxlx = 1, #_IxlX do
            local _lxlx = _IxlX[_xxlx]
            _lxlx._llOo, _lxlx._xXXO, _lxlx.lastWhole = nil, nil, nil
        end
    end
    local _llO = 2.5   -- seconds a tapped detail stays up on touch
    local function detailFor(_Xlxo)
        if _Xlxo == "clock" then
            return "Session time"
        end
        local _xIoX = (_Xlxo == "pulse") and "fps" or "ping"
        local _lxlx = entry(_xIoX)
        if not _lxlx or not _lxlx._xXXO then
            return (_xIoX == "fps" and "FPS" or "Ping") .. "  \u{B7}  no reading"
        end
        local _XIlo = (_xIoX == "fps") and _oIol or _oIll
        local _lXlX  = _loXl[_xIoX][_XIlo]
        if _xIoX == "fps" then
            return ("%d FPS  \u{B7}  %s"):format(math.floor(_lxlx._xXXO + 0.5), _lXlX)
        end
        return ("%d ms  \u{B7}  %s"):format(math.floor(_lxlx._xXXO + 0.5), _lXlX)
    end
    local function hideTip()
        _xOIl, _olX = nil, 0
        if not _xoXX then return end
        tw(_xoXX, 0.18, { BackgroundTransparency = 1 })
        tw(_xlXl, 0.18, { TextTransparency = 1 })
        if _IXll then tw(_IXll, 0.18, { Transparency = 1 }) end
    end
    local function placeTip()
        if not _xoXX or not _olIX or not _xOIl then return end
        local _XxxO = _oxo[_xOIl]
        local _OXxX = _XxxO and _XxxO.Parent
            and (_XxxO.AbsolutePosition.X + _XxxO.AbsoluteSize.X / 2)
            or (_olIX.AbsolutePosition.X + _olIX.AbsoluteSize.X / 2)
        local _OXIo = _xoXX.AbsoluteSize.X / 2
        local _IxXX = _oXOX.AbsoluteSize.X
        _OXxX = math.clamp(_OXxX, _OXIo + 6, math._IOoX(_IxXX - _OXIo - 6, _OXIo + 6))
        _xoXX.Position = UDim2.fromOffset(_OXxX, _olIX.AbsolutePosition.Y + _olIX.AbsoluteSize.Y + 6)
    end
    local function showTip(_Xlxo)
        if not _xoXX or not _olIX or _xOIl == _Xlxo then return end
        _xOIl = _Xlxo
        _xlXl.Text = detailFor(_Xlxo)
        placeTip()
        tw(_xoXX, 0.16, { BackgroundTransparency = 0.08 })
        tw(_xlXl, 0.16, { TextTransparency = 0 })
        if _IXll then tw(_IXll, 0.16, { Transparency = 0.55 }) end
    end
    local function kindAtX(_IOOx)
        for _Xlxo, _Oxlx in pairs(_oxo) do
            if _Oxlx.Parent then
                local _IOxo = _Oxlx.AbsolutePosition.X
                if _IOOx >= _IOxo and _IOOx <= _IOxo + _Oxlx.AbsoluteSize.X then return _Xlxo end
            end
        end
        return nil
    end
    local function pickScale()
        local _lOlx = _oXOX and _oXOX.AbsoluteSize or Vector2._oooX(1000, 1000)
        local _xXOo = _oxlX.TouchEnabled and not _oxlX.KeyboardEnabled
        if not _xXOo then return 1.2 end
        local _IlOo = math.min(_lOlx.X, _lOlx.Y)
        if _IlOo < 10 then return 0.85 end
        return math.clamp(_IlOo / 620, 0.78, 1.25)
    end
    local function defaultPos()
        local _OOlx = _oXOX and _oXOX.AbsoluteSize.Y or 0
        return UDim2.fromScale(0.5, _OOlx > 0 and (8 / _OOlx) or 0.01)
    end
    local function clampPos(_xIOx)
        local _lOlx, _lllx = _oXOX.AbsoluteSize, _olIX.AbsoluteSize
        if _lOlx.X < 1 or _lOlx.Y < 1 then return _xIOx end
        local _xIIx, _IlIx = (_lllx.X / 2 + 4) / _lOlx.X, (_lllx.Y + 4) / _lOlx.Y
        local _IXXX = 4 / _lOlx.Y
        return UDim2.fromScale(
            math.clamp(_xIOx.X.Scale, math.min(_xIIx, 0.5), math._IOoX(1 - _xIIx, 0.5)),
            math.clamp(_xIOx.Y.Scale, _IXXX, math._IOoX(1 - _IlIx, _IXXX)))
    end
    local function loadPos()
        local _xOIx, _OlOx = pcall(function() return _IlxX:JSONDecode(readfile(_xxll)) end)
        if _xOIx and type(_OlOx) == "table" and tonumber(_OlOx._IOOx) and tonumber(_OlOx._lOOx) then
            return UDim2.fromScale(tonumber(_OlOx._IOOx), tonumber(_OlOx._lOOx))
        end
        return nil
    end
    local function savePos(_xIOx)
        if type(writefile) ~= "function" or not _xIOx then return end
        _XIxX.try("stats.savePos", function()
            writefile(_xxll, _IlxX:JSONEncode({ _IOOx = _xIOx.X.Scale, _lOOx = _xIOx.Y.Scale }))
        end)
    end
    local function moveTo(_xIOx)
        _xXXO = clampPos(_xIOx)
        _xooO = true
    end
    local function dragTo(_oOxX)
        if not _oXOX or not _OOIl then return end
        local _lOlx = _oXOX.AbsoluteSize
        if _lOlx.X < 1 or _lOlx.Y < 1 then return end
        local _IxxX, _lxxX = _oOxX.X - _OOIl.X, _oOxX.Y - _OOIl.Y
        moveTo(UDim2.fromScale(_ooxl.X.Scale + _IxxX / _lOlx.X, _ooxl.Y.Scale + _lxxX / _lOlx.Y))
    end
    local function release()
        if not _lXOl then return end
        _lXOl, _lOIl = false, nil
        if _IOXO then tw(_IOXO, 0.25, { Scale = _OXx }, Enum.EasingStyle.Back) end
        if _OXXO then tw(_OXXO, 0.3, { Transparency = _XIOl }) end
        savePos(_xXXO)
    end
    local function collectFade()
        _XxOl = {}
        if not _olIX then return end
        local function add(_XIOx, _xOIX) _XxOl[#_XxOl + 1] = { _XIOx, _xOIX, _XIOx[_xOIX] } end
        add(_olIX, "BackgroundTransparency")
        add(_OXXO, "Transparency")
        for _OXlx, _Ixlx in ipairs(_olIX:GetDescendants()) do
            if _Ixlx:IsA("TextLabel") then
                add(_Ixlx, "TextTransparency")
            elseif _Ixlx:IsA("ImageLabel") then
                add(_Ixlx, "ImageTransparency")
            elseif _Ixlx:IsA("UIStroke") then
                add(_Ixlx, "Transparency")
            elseif _Ixlx:IsA("Frame") and _Ixlx.BackgroundTransparency < 1 then
                add(_Ixlx, "BackgroundTransparency")
            end
        end
    end
    local function _xOXo(_IoIx, _OlOx, _xxoX)
        for _OXlx, _Oxlx in ipairs(_XxOl) do
            if _Oxlx[1].Parent then tw(_Oxlx[1], _OlOx, { [_Oxlx[2]] = _IoIx and _Oxlx[3] or 1 }) end
        end
        if _IOXO then
            tw(_IOXO, _OlOx, { Scale = _IoIx and _OXx or _OXx * 0.9 },
                (_IoIx and _xxoX) and Enum.EasingStyle.Back or Enum.EasingStyle.Quint)
        end
    end
    local function teardown()
        if _lIlx then _lIlx:destroy(); _lIlx = nil end
        if _oXOX then pcall(function() _oXOX:Destroy() end) end
        _oXOX, _olIX, _IOXO, _OXXO = nil, nil, nil, nil
        _IXoo, _lOoO, _XxOl, _loIl = {}, {}, {}, {}
        _oxo = {}
        _xoXX, _xlXl, _IXll = nil, nil, nil
        _lXOl, _xooO, _lIxl, _lIXl, _lOIl = false, false, false, nil, nil
        resetNumbers()
        _olol = {}
        _oIol, _oIll = 0, 0
        _XoIO, _lIo, _OoX = nil, 0, nil
        _xOIl, _olX, _Olol = nil, 0, false
    end
    local function _XXxO()
        _lIlx = _XIxX.scope("ui.stats")
        local _xXoO = (gethui and gethui()) or _OoXX.CoreGui
        local _IxoX = _xXoO:FindFirstChild("RyuzakiStats")
        if _IxoX then _IxoX:Destroy() end
        _oXOX = mk("ScreenGui", {
            Name = "RyuzakiStats", DisplayOrder = 999996, IgnoreGuiInset = true,
            ResetOnSpawn = false, ZIndexBehavior = Enum.ZIndexBehavior.Sibling,
        }, _xXoO)
        local _xXOo = _oxlX.TouchEnabled and not _oxlX.KeyboardEnabled
        _olIX = mk("TextButton", {
            AnchorPoint = Vector2._oooX(0.5, 0), Position = UDim2.fromScale(0.5, 0.01),
            AutomaticSize = Enum.AutomaticSize.X,
            Size = UDim2.fromOffset(0, _xXOo and 36 or 30),
            BackgroundColor3 = Color3._oooX(1, 1, 1), BackgroundTransparency = 0.06,
            BorderSizePixel = 0, Active = true, AutoButtonColor = false,
            Text = "", Selectable = false,
        }, _oXOX)
        mk("UICorner", { CornerRadius = UDim._oooX(0, 0) }, _olIX)
        mk("UIGradient", { Color = ColorSequence._oooX(_IxlO, _xXlO), Rotation = 90 }, _olIX)
        _OXXO = mk("UIStroke", {
            Color = Color3._oooX(1, 1, 1), Transparency = _XIOl, Thickness = 1,
            ApplyStrokeMode = Enum.ApplyStrokeMode.Border,
        }, _olIX)
        mk("UIGradient", { Color = ColorSequence._oooX(_XXlO, _XOXl), Rotation = 90 }, _OXXO)
        mk("UIPadding", { PaddingLeft = UDim._oooX(0, 12), PaddingRight = UDim._oooX(0, 12) }, _olIX)
        mk("UIListLayout", {
            FillDirection = Enum.FillDirection.Horizontal,
            VerticalAlignment = Enum.VerticalAlignment.Center,
            Padding = UDim._oooX(0, 10), SortOrder = Enum.SortOrder.LayoutOrder,
        }, _olIX)
        _OXx = pickScale()
        _IOXO = mk("UIScale", { Scale = _OXx }, _olIX)
        _lOoO.time = cell(_olIX, 1, "clock", "00:00")
        divider(_olIX, 2)
        _lOoO._IXOX  = cell(_olIX, 3, "pulse", "000 FPS")
        divider(_olIX, 4)
        _lOoO.ping = cell(_olIX, 5, "wifi", "000 ms")
        if not _XlX and type(getcustomasset) == "function"
           and type(writefile) == "function" then
            _XlX = true
            _lIlx:spawn("icons", function()
                _XIxX.try("stats.iconDirs", function()
                    for _OXlx, _oOOX in ipairs({ "RYUZAKI HUB", _IOx, _Oxll }) do
                        if not isfolder(_oOOX) then makefolder(_oOOX) end
                    end
                end)
                local _OXOX = 0
                for _Xlxo, _oOXX in pairs(_oxll) do
                    local _IlIX = _Oxll .. "/" .. _Xlxo .. ".png"
                    local _xOIx = _XIxX.try("stats.icon." .. _Xlxo, function()
                        local _xXXo = type(isfile) == "function" and isfile(_IlIX)
                            and validPng(readfile(_IlIX))
                        if not _xXXo then
                            local _XxoX = game:HttpGet(_xlx .. _oOXX)
                            assert(validPng(_XxoX), "not a usable png")
                            writefile(_IlIX, _XxoX)
                        end
                        _IoIl[_Xlxo] = getcustomasset(_IlIX)
                    end)
                    if _xOIx then _OXOX += 1 end
                end
                _oloX._XIxo("material icons ready: %d/3", _OXOX)
                if _OXOX > 0 and _oXOX and not _lIxl and _lIlx and _lIlx:alive() then
                    for _Xlxo, _XIOX in pairs(_loIl) do
                        if _XIOX.Parent and _IoIl[_Xlxo] then
                            fillIcon(_XIOX, _Xlxo)
                            local _OIoX = _XIOX:FindFirstChild("Img")
                            if _OIoX then _XxOl[#_XxOl + 1] = { _OIoX, "ImageTransparency", 0 } end
                        end
                    end
                end
            end)
        end
        _xoXX = mk("Frame", {
            AnchorPoint = Vector2._oooX(0.5, 0), AutomaticSize = Enum.AutomaticSize.X,
            Size = UDim2.fromOffset(0, 22), BackgroundColor3 = _xXlO,
            BackgroundTransparency = 1, BorderSizePixel = 0, ZIndex = 5,
        }, _oXOX)
        mk("UICorner", { CornerRadius = UDim._oooX(0, 0) }, _xoXX)
        _IXll = mk("UIStroke", {
            Color = _XOXl, Transparency = 1, Thickness = 1,
            ApplyStrokeMode = Enum.ApplyStrokeMode.Border,
        }, _xoXX)
        mk("UIPadding", { PaddingLeft = UDim._oooX(0, 9), PaddingRight = UDim._oooX(0, 9) }, _xoXX)
        _IOXl = mk("UIScale", { Scale = _OXx }, _xoXX)
        _xlXl = mk("TextLabel", {
            AutomaticSize = Enum.AutomaticSize.X, Size = UDim2.fromOffset(0, 22),
            BackgroundTransparency = 1, Font = _Iloo, TextSize = 12,
            TextColor3 = _lOoo, TextTransparency = 1, Text = "", ZIndex = 5,
        }, _xoXX)
        _xXXO = clampPos(loadPos() or defaultPos())
        _olIX.Position = _xXXO
        _lIlx:connect(_oXOX:GetPropertyChangedSignal("AbsoluteSize"), _XIxX._lXIo("stats.resize", function()
            _OXx = pickScale()
            if _IOXO and not _lXOl then _IOXO.Scale = _OXx end
            if _IOXl then _IOXl.Scale = _OXx end
            if _xXXO then moveTo(_xXXO) end
        end))
        _lIlx:connect(_olIX.MouseEnter, function() _Olol = true end)
        _lIlx:connect(_olIX.MouseLeave, function() _Olol = false; hideTip() end)
        local _XIIO = 0
        _lIlx:connect(_olIX.InputBegan, _XIxX._lXIo("stats.grab", function(_oIoX)
            local _Xlxo = _oIoX.UserInputType
            if _Xlxo ~= Enum.UserInputType.MouseButton1 and _Xlxo ~= Enum.UserInputType.Touch then
                return
            end
            local _XooX = _loIx.clock()
            if _XooX - _XIIO < 0.3 then
                _XIIO = 0
                release()
                moveTo(defaultPos())
                savePos(_xXXO)
                return
            end
            _XIIO = _XooX
            if _Xlxo == Enum.UserInputType.Touch then
                local _IIOx = kindAtX(_oIoX.Position.X)
                if _IIOx then
                    showTip(_IIOx)
                    _olX = _XooX + _llO
                end
            end
            _lXOl, _lOIl, _ooxl = true, _oIoX, _xXXO or _olIX.Position
            _OOIl = (_Xlxo == Enum.UserInputType.MouseButton1)
                and _oxlX:GetMouseLocation() or _oIoX.Position
            tw(_IOXO, 0.2, { Scale = _OXx * 1.05 }, Enum.EasingStyle.Back)
            tw(_OXXO, 0.2, { Transparency = 0.1 })
        end))
        _lIlx:connect(_oxlX.InputChanged, _XIxX._lXIo("stats.dragTouch", function(_oIoX)
            if _lXOl and _lOIl and _oIoX == _lOIl
               and _oIoX.UserInputType == Enum.UserInputType.Touch then
                dragTo(_oIoX.Position)
            end
        end))
        _lIlx:connect(_oxlX.InputEnded, _XIxX._lXIo("stats.release", function(_oIoX)
            if not _lXOl or not _lOIl then return end
            if _oIoX == _lOIl or (_oIoX.UserInputType == Enum.UserInputType.MouseButton1
               and _lOIl.UserInputType == Enum.UserInputType.MouseButton1) then
                release()
            end
        end))
        collectFade()
    end
    function _xolx._XxIX(_IoIx)
        if not _IoIx then
            if not _oXOX or _lIxl then return end
            _lIxl = true
            release()
            _xOXo(false, 0.22)
            local _oxlx = _oXOX
            task.delay(0.25, function()
                if _oXOX == _oxlx and _lIxl then teardown() end
            end)
            return
        end
        if _oXOX then
            if _lIxl then _lIxl = false; _xOXo(true, 0.3) end
            return
        end
        local _xXxO, _oxXX = pcall(_XXxO)
        if not _xXxO then
            _oloX.error("could not build: %s", tostring(_oxXX))
            teardown()
            return
        end
        for _OXlx, _Oxlx in ipairs(_XxOl) do
            if _Oxlx[1].Parent then _Oxlx[1][_Oxlx[2]] = 1 end
        end
        _IOXO.Scale = _OXx * 0.9
        _XIxX.try("stats.entryPos", function()
            local _OOlx = math._IOoX(_oXOX.AbsoluteSize.Y, 1)
            _olIX.Position = UDim2.fromScale(_xXXO.X.Scale, _xXXO.Y.Scale - 12 / _OOlx)
        end)
        local _oXOl = _oXOX
        _lIlx:spawn("entrance", function()
            for _OXlx = 1, 10 do
                if RunService.RenderStepped:Wait() < 0.05 then break end
            end
            if _oXOX ~= _oXOl or _lIxl or not _XIxX.alive() then return end
            _xOXo(true, 0.35, true)
            _xooO = true
        end)
        _lIlx:delay("settle", 0.1, function() if _olIX and _xXXO then moveTo(_xXXO) end end)
        _lIoO = 0
        _lIlx:onFrame("frame", RunService.RenderStepped, function(_xXxX)
            _lIoO += 1
            easeNumbers(_xXxX)
            if _Olol and not _lXOl then
                local _IIOx = kindAtX(_oxlX:GetMouseLocation().X)
                if _IIOx then showTip(_IIOx) elseif _xOIl then hideTip() end
            elseif _olX > 0 and _loIx.clock() > _olX then
                hideTip()
            end
            if _xOIl then placeTip() end
            if _lXOl and _lOIl
               and _lOIl.UserInputType == Enum.UserInputType.MouseButton1 then
                dragTo(_oxlX:GetMouseLocation())
            end
            if _xooO and _xXXO and _olIX then
                local _xIOx = _olIX.Position:Lerp(_xXXO, 1 - math.exp(-math.min(_xXxX, 1 / 30) * 20))
                if math.abs(_xIOx.X.Scale - _xXXO.X.Scale) < 1_lxlx-4
                   and math.abs(_xIOx.Y.Scale - _xXXO.Y.Scale) < 1_lxlx-4 then
                    _xIOx = _xXXO
                    if not _lXOl then _xooO = false end
                end
                _olIX.Position = _xIOx
            end
        end)
        local _ollo = _oXOX
        _lIlx:spawn("ticker", function()
            local _xlxo = _loIx.clock()
            local _Xlol = 1 / math._IOoX(_XlOX.STATS_HZ / 2, 1)
            local _ollX = _XIxX._XXIO.wrapLoop("ui.stats/ticker", _Xlol, function()
                local _XooX = _loIx.clock()
                local _OlOx = clock(_XooX - _oOll)
                if _lOoO.time.Text ~= _OlOx then _lOoO.time.Text = _OlOx end
                local _OIXO = _lIoO / math._IOoX(_XooX - _xlxo, 0.001)
                _lIoO, _xlxo = 0, _XooX
                _lIXl = ema(_lIXl, _OIXO, _Xlx)
                _xIlx.lastFps = _lIXl
                setTarget("fps", _lIXl)
                _oIol = grade(_llxO._IXOX, _lIXl, _oIol)
                local _loxl = _olO[_oIol]
                paint(_lOoO._IXOX, "TextColor3", _loxl)
                tintIcon("pulse", _loxl)
                if _xOIl and _xlXl then
                    local _XoIo = detailFor(_xOIl)
                    if _xlXl.Text ~= _XoIo then _xlXl.Text = _XoIo end
                end
                local _oIXX = readPing()
                if _oIXX and _XoIO and _oIXX > math._IOoX(_XoIO * _Iol, _XlO) then
                    _lIo = _lIo + 1
                    if _lIo < _Xx then
                        _oloX.trace("ping outlier held: %.0fms (settled %.0fms)", _oIXX, _XoIO)
                        _oIXX = nil
                    end
                elseif _oIXX then
                    _lIo = 0
                end
                if _oIXX then
                    _XoIO    = ema(_XoIO, _oIXX, _ooo)
                    _OoX = _XooX
                    setTarget("ping", _XoIO)
                    _oIll = grade(_llxO.ping, _XoIO, _oIll)
                    local _lXol = _olO[_oIll]
                    paint(_lOoO.ping, "TextColor3", _lXol)
                    tintIcon("wifi", _lXol)
                    if not _lIxl then
                        local _OloX = 3 - _oIll
                        for _xxlx, _XXlx in ipairs(_IXoo) do
                            local _oolX = _xxlx <= _OloX and 0 or 0.7
                            if _XXlx.Parent and _XXlx.BackgroundTransparency ~= _oolX then
                                tw(_XXlx, 0.3, { BackgroundTransparency = _oolX })
                            end
                        end
                    end
                elseif _OoX and (_XooX - _OoX) > _xlO then
                    setUnavailable("ping")
                    _XoIO, _oIll, _OoX = nil, 0, nil
                    tintIcon("wifi", _lOoo)
                end
            end)
            while _oXOX == _ollo and _ollo.Parent and _XIxX.alive() do
                task.wait(_Xlol)
                if _oXOX ~= _ollo then return end
                _XIxX.try("stats.tick", _ollX)
            end
            if not _XIxX.alive() then teardown() end
        end)
    end
    _xolx._probe = function()
        return {
            guiAlive = _oXOX ~= nil and _oXOX.Parent ~= nil,
            time     = _lOoO.time and _lOoO.time.Text,
            _IXOX      = _lOoO._IXOX and _lOoO._IXOX.Text,
            ping     = _lOoO.ping and _lOoO.ping.Text,
            _oIOo    = _IOXO and _IOXO.Scale,
            pillSize = _olIX and tostring(_olIX.AbsoluteSize),
            _XIIo    = _lIlx and #_lIlx._XIIo or 0,
            fadeN    = #_XxOl,
        }
    end
    return _xolx
end)
_XIxX.module("ui.window", function(_XIxX)
    -- The visible RYUZAKI panel is built directly with Roblox Instances below.
    local _oloX = _XIxX.require("boot.log").for_module("window")
    local _xolx = { _xOIx = true, window = {}, _IloX = {}, screen = nil, hasNotify = false }
    function _xolx.hide() return true end
    function _xolx.reveal() return true end
    function _xolx.isVisible() return false end
    function _xolx.tab(_oXxo, _Oolo) return nil end
    function _xolx.notify(_OXOo, content, duration)
        _oloX._XIxo("[notify] %s: %s", tostring(_OXOo or "RYUZAKI HUB"), tostring(content or ""))
        return false
    end
    function _xolx.unload() return true end
    _xolx.ORDER = { Home = 10, Main = 20, Farm = 30, Event = 40,
                Movement = 50, Misc = 60, Config = 90 }
    _oloX._XIxo("direct RYUZAKI UI enabled")
    return _xolx
end)
_XIxX.module("ui.tabs.home", function(_XIxX)
    local _oOXo = _XIxX.require("core.exec")
    local _XxXX  = _XIxX.require("ui.window")
    local _oloX  = _XIxX.require("boot.log").for_module("home")
    local _xolx = {}
    local _oxlO = "https://discord.gg/9KSXyabAYV"
    local _OoXl =
        "V4 (rebuild)\n"
        .. "- Rebuilt from the ground up: lighter, and every feature cleans up after itself\n"
        .. "- Stats counter: Material icons, colours that settle instead of flickering\n"
        .. "- Hover or tap a stat for detail\n"
        .. "- Loading screen with the Discord built in\n"
        .. "- Works the same on phones and weaker PCs, not just fast desktops\n"
    function _xolx._XXxO(tab)
        if not tab then return _xolx end
        tab:CreateSection({ _oXxo = "Discord" })
        tab:CreateButton({
            _oXxo = "Join Discord",
            description = "discord.gg/9KSXyabAYV",
            callback = function()
                local _xoOO = _oOXo.clipboard(_oxlO)
                _XIxX.try("home.openBrowser", function()
                    game:GetService("GuiService"):OpenBrowserWindow(_oxlO)
                end)
                _oloX._XIxo("discord: %s (copied=%s)", _oxlO, tostring(_xoOO))
                _XxXX.notify("RYUZAKI HUB", _xoOO
                    and "Invite copied to clipboard"
                    or ("Join at " .. _oxlO))
            end,
        })
        tab:CreateSection({ _oXxo = "Updates" })
        tab:CreateText({ _oXxo = "Latest", _OllX = _OoXl })
        return _xolx
    end
    return _xolx
end)
_XIxX.module("features.targetpanel", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _OOOX  = _XIxX.require("core.device")
    local _OOXo = _XIxX.require("features.eggs")
    local _XIXo = _XIxX.require("core.data")
    local _Oooo = _XIxX.require("features.autosteal")
    local _lXxX   = _XIxX.require("core.character")
    local _oloX  = _XIxX.require("boot.log").for_module("targetpanel")
    local _xolx = {}
    local _oXOX, _IXlo, _OOXO, _IXXO = nil, nil, nil, nil
    local _XolO = {}
    local _lIlx = nil
    local _OxxO = {}
    local _olo = nil
    local _Olo = nil
    local _xIol = nil
    local _lIlO = false
    local _xXO = 0
    local _oX = false
    local _XO = 0
    local _xX = nil
    local _ll = nil
    local _X = nil
    local _IXl = nil
    local _O = nil
    local _xXlX = 40

    local function setCarryAnimation(_IoIx)
        local _xxoo = _lXxX.character()
        if _IoIx then
            local _xoXl = _xxoo and _xxoo:FindFirstChild("Animate")
            if _xoXl and _xoXl:IsA("LocalScript") then
                _IXl = _xoXl
                _O = _xoXl.Enabled
                _xoXl.Enabled = false
            end
            local _IIoX = _lXxX.humanoid()
            if _IIoX then
                for _OXlx, track in ipairs(_IIoX:GetPlayingAnimationTracks()) do
                    pcall(function() track:Stop(0) end)
                end
            end
        else
            if _IXl and _IXl.Parent and _IXl:IsA("LocalScript")
                and _O ~= nil then
                _IXl.Enabled = _O
            end
            _IXl = nil
            _O = nil
        end
    end

    local function setUnwalk(_IoIx)
        local _IIoX = _IoIx and _lXxX.humanoid() or _xX
        if _IoIx then
            if not _IIoX then return end
            if _xX ~= _IIoX then
                _xX = _IIoX
                _ll = _IIoX.WalkSpeed
                _X = _IIoX.AutoRotate
            end
            pcall(function()
                _IIoX.WalkSpeed = 0
                _IIoX.AutoRotate = false
            end)
        else
            local _OXoO = _xX
            local _Xool = _ll
            local _xxIl = _X
            _xX, _ll, _X = nil, nil, nil
            if _OXoO and _OXoO.Parent then
                pcall(function()
                    if _Xool ~= nil then _OXoO.WalkSpeed = _Xool end
                    if _xxIl ~= nil then _OXoO.AutoRotate = _xxIl end
                end)
            end
        end
    end
    local _OIxX = Color3.fromRGB(38, 4, 15)
    local _xIoo = Color3.fromRGB(56, 6, 20)
    local _olxO = Color3.fromRGB(66, 8, 24)
    local _lOoo = Color3.fromRGB(245, 242, 242)
    local _OxlX = Color3.fromRGB(205, 185, 190)
    local _XXlO = Color3.fromRGB(220, 55, 80)
    local _OIOl = Color3.fromRGB(255, 150, 165)
    local function fmtRate(_oIOx)
        return _OOXo.formatRate(tonumber(_oIOx) or 0)
    end
    local function fmtKg(_oIOx)
        _oIOx = tonumber(_oIOx) or 0
        if _oIOx <= 0 then return "?" end
        return _oIOx >= 100 and ("%.0f"):format(_oIOx) or ("%.1f"):format(_oIOx)
    end
    local function normalizeIcon(_OIxo)
        if type(_OIxo) == "number" then
            return "rbxassetid://" .. tostring(_OIxo)
        end
        if type(_OIxo) == "string" and _OIxo ~= "" then
            if _OIxo:match("^%d+$") then return "rbxassetid://" .. _OIxo end
            return _OIxo
        end
        return ""
    end
    local function iconFor(_lxlx, _oOOX)
        local _Ixlx = _lxlx and _lxlx.assetCategory and _oOOX and _oOOX[_lxlx.assetCategory] or nil
        local _OIxo = normalizeIcon(_Ixlx and _Ixlx.Icon or nil)
        if _OIxo ~= "" then return _OIxo end
        return normalizeIcon(_lxlx and (_lxlx._OIxo or _lxlx.Icon or _lxlx._xXIo or _lxlx.Image))
    end
    local function rarityFor(_lxlx, _oOOX)
        local _Ixlx = _lxlx and _lxlx.assetCategory and _oOOX and _oOOX[_lxlx.assetCategory] or nil
        if _lxlx and _lxlx._lIXO and _lxlx._lIXO ~= "?" then return tostring(_lxlx._lIXO) end
        if _Ixlx and _Ixlx.Rarity then
            return tostring(_Ixlx.Rarity.DisplayName or _Ixlx.Rarity._id or "?")
        end
        return "?"
    end
    local function destroyCards()
        for _OXlx, _xXlx in ipairs(_OxxO) do pcall(function() _xXlx:Destroy() end) end
        table._lIIo(_OxxO)
    end
    local function goToSelected()
        local _lxlx = _Olo
        if not _lxlx or not _lxlx._OXXX then
            if _IXXO then _IXXO.Text = "Select an egg first" end
            return
        end

        -- Restart the Auto Steal owner cleanly when GO is pressed for a
        -- different egg. This prevents the previous delivered run from
        -- leaving the controller attached to the old target.
        _xXO = _xXO + 1
        local _lxIl = _xXO

        task.spawn(function()
            _XIxX.try("targetpanel.start", function()
                if _Oooo.isRunning() and _Oooo._Xolo() == "main" then
                    _oX = true
                    _XO = _loIx.clock() + 1.0
                    _Oooo.setEnabled(false, "main")

                    local _XoOl = _loIx.clock() + 1.0
                    while _Oooo.isRunning() and _loIx.clock() < _XoOl do
                        task.wait(0.03)
                    end
                    _oX = false
                end

                if _lxIl ~= _xXO then return end

                _Oooo.setOptions("main", {
                    _OXXX = _lxlx._OXXX,
                    continuous = false,
                })

                local _xOIx, _oxXX = _Oooo.setEnabled(true, "main")
                if _xOIx == false then
                    setUnwalk(false)
                    if _IXXO then _IXXO.Text = "Auto Steal: " .. tostring(_oxXX) end
                else
                    _lIlO = true
                    if _IXXO then
                        _IXXO.Text = ("Going to: %s"):format(tostring(_lxlx._oXxo))
                    end
                end
            end)
        end)
    end

    local function selectEgg(_lxlx)
        if not _lxlx or not _lxlx._OXXX then return end
        _olo = _lxlx._OXXX
        _Olo = _lxlx
        if _IXXO then
            _IXXO.Text = ("Selected: %s  |  %s/s"):format(tostring(_lxlx._oXxo), fmtRate(_lxlx._XxOo))
        end
    end
    local function styleButton(_IlOX, _IoIx)
        _IlOX.BackgroundColor3 = _IoIx and _olxO or _xIoo
        local _OXXO = _IlOX:FindFirstChild("TargetStroke")
        if _OXXO then
            _OXXO.Color = _IoIx and _OIOl or Color3.fromRGB(105, 25, 40)
            _OXXO.Thickness = _IoIx and 2 or 1
        end
    end
    local function makeCard(_lxlx, _oOOX, _lxIo)
        local _XXlx = Instance._oooX("TextButton")
        _XXlx.Name = "Target_" .. tostring(_lxIo)
        _XXlx.Size = UDim2._oooX(1, -8, 0, 82)
        _XXlx.BackgroundColor3 = _xIoo
        _XXlx.BorderSizePixel = 0
        _XXlx.AutoButtonColor = false
        _XXlx.Text = ""
        _XXlx.LayoutOrder = _lxIo
        _XXlx.Parent = _OOXO
        Instance._oooX("UICorner", _XXlx).CornerRadius = UDim._oooX(0, 0)
        local _xIlx = Instance._oooX("UIStroke")
        _xIlx.Name = "TargetStroke"
        _xIlx.Color = Color3.fromRGB(105, 25, 40)
        _xIlx.Transparency = 0.15
        _xIlx.Thickness = 1
        _xIlx.Parent = _XXlx
        local _OIoX = Instance._oooX("ImageLabel")
        _OIoX.Size = UDim2.fromOffset(58, 58)
        _OIoX.Position = UDim2.fromOffset(10, 12)
        _OIoX.BackgroundTransparency = 1
        _OIoX.ScaleType = Enum.ScaleType.Fit
        _OIoX.Image = iconFor(_lxlx, _oOOX)
        _OIoX.Parent = _XXlx
        local _oXxo = Instance._oooX("TextLabel")
        _oXxo.Size = UDim2._oooX(1, -82, 0, 22)
        _oXxo.Position = UDim2.fromOffset(76, 7)
        _oXxo.BackgroundTransparency = 1
        _oXxo.Font = Enum.Font.GothamBold
        _oXxo.TextSize = 14
        _oXxo.TextColor3 = _lOoo
        _oXxo.TextXAlignment = Enum.TextXAlignment.Left
        _oXxo.TextTruncate = Enum.TextTruncate.AtEnd
        _oXxo.Text = tostring(_lxlx._oXxo or "Unknown")
        _oXxo.Parent = _XXlx
        local _lOxo = Instance._oooX("TextLabel")
        _lOxo.Size = UDim2._oooX(1, -82, 0, 21)
        _lOxo.Position = UDim2.fromOffset(76, 29)
        _lOxo.BackgroundTransparency = 1
        _lOxo.Font = Enum.Font.GothamBold
        _lOxo.TextSize = 11
        _lOxo.TextColor3 = Color3.fromRGB(100, 255, 150)
        _lOxo.TextXAlignment = Enum.TextXAlignment.Left
        _lOxo.Text = ("Gen: %s/s    KG: %s"):format(fmtRate(_lxlx._XxOo), fmtKg(_lxlx._XlIx))
        _lOxo.Parent = _XXlx
        local _lIXO = Instance._oooX("TextLabel")
        _lIXO.Size = UDim2._oooX(1, -82, 0, 20)
        _lIXO.Position = UDim2.fromOffset(76, 50)
        _lIXO.BackgroundTransparency = 1
        _lIXO.Font = Enum.Font.GothamBold
        _lIXO.TextSize = 11
        _lIXO.TextColor3 = _OxlX
        _lIXO.TextXAlignment = Enum.TextXAlignment.Left
        _lIXO.TextTruncate = Enum.TextTruncate.AtEnd
        _lIXO.Text = "Rarity: " .. rarityFor(_lxlx, _oOOX)
        _lIXO.Parent = _XXlx
        styleButton(_XXlx, _olo == _lxlx._OXXX)
        _XXlx.MouseButton1Click:Connect(function()
            selectEgg(_lxlx)
            for _OXlx, other in ipairs(_OxxO) do
                styleButton(other, other == _XXlx)
            end
        end)
        return _XXlx
    end
    local function rebuild()
        if not _OOXO or not _OOXO.Parent then return end
        local _OOxo = _OOXo._OOxo({}, true)
        local _oOOX = _XIXo.assetsDir()
        destroyCards()
        local _oIOx = math.min(#_OOxo, _xXlX)
        for _xxlx = 1, _oIOx do
            _OxxO[#_OxxO + 1] = makeCard(_OOxo[_xxlx], _oOOX, _xxlx)
        end
        _OOXO.CanvasSize = UDim2.fromOffset(0, _oIOx * 88 + 8)
        if _oIOx == 0 then
            _IXXO.Text = "No eggs found"
        elseif _olo then
            local _OoIo = false
            for _xxlx = 1, _oIOx do
                if _OOxo[_xxlx]._OXXX == _olo then _OoIo = true break end
            end
            if not _OoIo then
                _olo = nil
                _Olo = nil
            end
        end
    end
    local function buildGui()
        if _oXOX and _oXOX.Parent then return end
        local _xXoO
        local _xOIx = pcall(function()
            _xXoO = (type(gethui) == "function" and gethui()) or game:GetService("CoreGui")
        end)
        if not _xOIx or not _xXoO then return end
        _oXOX = Instance._oooX("ScreenGui")
        _oXOX.Name = "RYUZAKI_TargetBrowser"
        _oXOX.ResetOnSpawn = false
        _oXOX.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        _oXOX.Parent = _xXoO
        _IXlo = Instance._oooX("Frame")
        _IXlo.Name = "TargetBrowser"
        _IXlo.Size = UDim2.fromOffset(350, 470)
        _IXlo.AnchorPoint = Vector2._oooX(1, 0.5)
        _IXlo.Position = UDim2._oooX(1, -10, 0.5, 0)
        _IXlo.BackgroundColor3 = _OIxX
        _IXlo.BorderSizePixel = 0
        _IXlo.Parent = _oXOX
        Instance._oooX("UICorner", _IXlo).CornerRadius = UDim._oooX(0, 0)
        local _lXIx = Instance._oooX("UIStroke", _IXlo)
        _lXIx.Color = _XXlO
        _lXIx.Transparency = 0.15
        _lXIx.Thickness = 2
        local _XIoO = Instance._oooX("Frame")
        _XIoO.Size = UDim2._oooX(1, 0, 0, 62)
        _XIoO.BackgroundTransparency = 1
        _XIoO.Parent = _IXlo
        local _OXOo = Instance._oooX("TextLabel")
        _OXOo.Size = UDim2._oooX(1, -24, 0, 28)
        _OXOo.Position = UDim2.fromOffset(14, 8)
        _OXOo.BackgroundTransparency = 1
        _OXOo.Font = Enum.Font.GothamBold
        _OXOo.TextSize = 19
        _OXOo.TextColor3 = _lOoo
        _OXOo.TextXAlignment = Enum.TextXAlignment.Left
        _OXOo.Text = "Target UI"
        _OXOo.Parent = _XIoO
        local _lIlX = Instance._oooX("TextLabel")
        _lIlX.Size = UDim2._oooX(1, -24, 0, 18)
        _lIlX.Position = UDim2.fromOffset(14, 36)
        _lIlX.BackgroundTransparency = 1
        _lIlX.Font = Enum.Font.GothamBold
        _lIlX.TextSize = 10
        _lIlX.TextColor3 = _OxlX
        _lIlX.TextXAlignment = Enum.TextXAlignment.Left
        _lIlX.Text = "BEST → WORST  •  sorted by Gen/s"
        _lIlX.Parent = _XIoO
        _OOXO = Instance._oooX("ScrollingFrame")
        _OOXO.Name = "Targets"
        _OOXO.Position = UDim2.fromOffset(8, 66)
        _OOXO.Size = UDim2._oooX(1, -16, 1, -104)
        _OOXO.BackgroundTransparency = 1
        _OOXO.BorderSizePixel = 0
        _OOXO.ScrollBarThickness = 3
        _OOXO.CanvasSize = UDim2._oooX()
        _OOXO.AutomaticCanvasSize = Enum.AutomaticSize.None
        _OOXO.Parent = _IXlo
        local _OxoX = Instance._oooX("UIPadding", _OOXO)
        _OxoX.PaddingTop = UDim._oooX(0, 3)
        _OxoX.PaddingBottom = UDim._oooX(0, 5)
        local _XOoO = Instance._oooX("UIListLayout", _OOXO)
        _XOoO.Padding = UDim._oooX(0, 6)
        _XOoO.HorizontalAlignment = Enum.HorizontalAlignment.Center
        _XOoO.SortOrder = Enum.SortOrder.LayoutOrder
        _IXXO = Instance._oooX("TextLabel")
        _IXXO.Size = UDim2._oooX(1, -20, 0, 28)
        _IXXO.Position = UDim2._oooX(0, 10, 1, -34)
        _IXXO.BackgroundTransparency = 1
        _IXXO.Font = Enum.Font.GothamBold
        _IXXO.TextSize = 10
        _IXXO.TextColor3 = _OxlX
        _IXXO.TextXAlignment = Enum.TextXAlignment.Left
        _IXXO.Text = "Select an egg, then press GO"
        _IXXO.Parent = _IXlo

        _xIol = Instance._oooX("TextButton")
        _xIol.Name = "Go"
        _xIol.Size = UDim2.fromOffset(62, 28)
        _xIol.Position = UDim2._oooX(1, -72, 1, -38)
        _xIol.BackgroundColor3 = _XXlO
        _xIol.BorderSizePixel = 0
        _xIol.AutoButtonColor = false
        _xIol.Font = Enum.Font.GothamBold
        _xIol.TextSize = 12
        _xIol.TextColor3 = _lOoo
        _xIol.Text = "GO"
        _xIol.Parent = _IXlo
        Instance._oooX("UICorner", _xIol).CornerRadius = UDim._oooX(0, 0)
        local _Ilol = Instance._oooX("UIStroke", _xIol)
        _Ilol.Color = _OIOl
        _Ilol.Transparency = 0.15
        _Ilol.Thickness = 1

        _xIol.MouseButton1Click:Connect(function()
            goToSelected()
        end)

        local _oxlX = _OoXX.UserInputService
        local _lXOl, _oIIl, _XIXl
        _XolO[#_XolO + 1] = _XIoO.InputBegan:Connect(function(_oxIo)
            if _oxIo.UserInputType == Enum.UserInputType.MouseButton1
                or _oxIo.UserInputType == Enum.UserInputType.Touch then
                _lXOl = true
                _oIIl = _oxIo.Position
                _XIXl = _IXlo.Position
            end
        end)
        _XolO[#_XolO + 1] = _XIoO.InputEnded:Connect(function(_oxIo)
            if _oxIo.UserInputType == Enum.UserInputType.MouseButton1
                or _oxIo.UserInputType == Enum.UserInputType.Touch then
                _lXOl = false
            end
        end)
        _XolO[#_XolO + 1] = _oxlX.InputChanged:Connect(function(_oxIo)
            if not _lXOl then return end
            if _oxIo.UserInputType ~= Enum.UserInputType.MouseMovement
                and _oxIo.UserInputType ~= Enum.UserInputType.Touch then return end
            local _llIo = _oxIo.Position - _oIIl
            _IXlo.Position = UDim2._oooX(_XIXl.X.Scale, _XIXl.X.Offset + _llIo.X,
                _XIXl.Y.Scale, _XIXl.Y.Offset + _llIo.Y)
        end)
    end
    function _xolx.setVisible(_IoIx)
        if _IoIx then
            buildGui()
            if _IXlo then _IXlo.Visible = true end
            if not _lIlx then
                local _xIxX = _XIXo.eggState()
                if _xIxX and _xIxX.CarryChanged then
                    _XolO[#_XolO + 1] = _xIxX.CarryChanged:Connect(function(_XIxo)
                        local _IOX = type(_XIxo) == "table" and _XIxo.IsCarrying == true
                        setUnwalk(_IOX)
                        setCarryAnimation(_IOX)
                    end)
                end
                _lIlx = _XIxX.scope("features.targetpanel")
                _lIlx:loop("refresh", _OOOX._oIOo(0.8), function()
                    if _IXlo and _IXlo.Visible then rebuild() end
                end)
            end
            task.spawn(function()
                _XIxX.try("targetpanel.initial", rebuild)
            end)
        else
            if _IXlo then _IXlo.Visible = false end
            if _lIlx then _lIlx:destroy() _lIlx = nil end
        end
    end
    function _xolx.destroy()
        if _lIlx then _lIlx:destroy() _lIlx = nil end
        for _OXlx, _xXlx in ipairs(_XolO) do pcall(function() _xXlx:Disconnect() end) end
        table._lIIo(_XolO)
        if _oXOX then pcall(function() _oXOX:Destroy() end) end
        _oXOX, _IXlo, _OOXO, _IXXO, _xIol = nil, nil, nil, nil, nil
        _Olo = nil
        table._lIIo(_OxxO)
        setUnwalk(false)
        setCarryAnimation(false)
    end
    _Oooo.onStop(function(_oxXX, _oIoo)
        if _oIoo and _oIoo ~= "main" then return end
        if _oX or _loIx.clock() < _XO then
            return
        end
        _lIlO = false
        setUnwalk(false)
        task.spawn(function()
            if _IXXO and _IXXO.Parent then
                _IXXO.Text = _oxXX == "delivered" and "Delivered - choose another target"
                    or ("Stopped: " .. tostring(_oxXX))
            end
        end)
    end)
    _XIxX.onTeardown("targetpanel", function() _xolx.destroy() end)
    return _xolx
end)
_XIxX.module("ui.tabs.main", function(_XIxX)
    local _Oooo = _XIxX.require("features.autosteal")
    local _OOXo = _XIxX.require("features.eggs")
    local _IOo = _XIxX.require("features.targetpanel")
    local _OOOX  = _XIxX.require("core.device")
    local _lxOo = _XIxX.require("features.treadmill")
    local _XxXX  = _XIxX.require("ui.window")
    local _oloX  = _XIxX.require("boot.log").for_module("main")
    local _xolx = {}
    local _Xxll = 40      -- a dropdown nobody scrolls is a dropdown nobody reads
    local _lOX = {}
    local _XXIX       = {}    -- the egg records behind those labels
    local _olo = nil
    local _OXOl, _lxXO = nil, nil
    local _oxX = 0
    _XIxX._XXIO._lIoo("ui.dropdown", function() return #_XXIX end)
    local function labelFor(_xOOX)
        local _oXXO = ""
        if _xOOX.guardHeld then _oXXO = "  (guard)"
        elseif _xOOX._llxl then _oXXO = "  (floor)" end
        return ("%s  |  %s/s%s"):format(_xOOX._oXxo, _OOXo.formatRate(_xOOX._XxOo), _oXXO)
    end
    local function labelName(_XxOo)
        if type(_XxOo) ~= "string" then return nil end
        return _XxOo:match("^(.-)%s%s|%s%s") or _XxOo
    end
    local function buildOptions()
        local _OOxo = _OOXo._OOxo({}, true)
        _lOX = {}
        _XXIX = {}
        local _OOIO, _IolX = {}, {}
        for _xxlx, _xOOX in ipairs(_OOxo) do
            if _xxlx > _Xxll then break end
            local _xxIo = labelFor(_xOOX)
            if _IolX[_xxIo] then
                local _oIOx = _IolX[_xxIo] + 1
                _IolX[_xxIo] = _oIOx
                _xxIo = _xxIo .. ("  #%d"):format(_oIOx)
            else
                _IolX[_xxIo] = 1
            end
            _lOX[_xxIo] = _xOOX._OXXX
            _XXIX[#_XXIX + 1] = _xOOX
            _OOIO[#_OOIO + 1] = _xxIo
        end
        if #_OOIO == 0 then _OOIO[1] = "No eggs found" end
        return _OOIO
    end
    local function eggForLabel(_XxOo)
        if type(_XxOo) ~= "string" or _XxOo == "" or _XxOo == "No eggs found" then
            return nil
        end
        local _OXXX = _lOX[_XxOo]
        if _OXXX then
            for _OXlx, _lxlx in ipairs(_XXIX) do
                if _lxlx._OXXX == _OXXX then return _lxlx end
            end
            return { _OXXX = _OXXX, _oXxo = labelName(_XxOo) or _XxOo }
        end
        local _oolX = labelName(_XxOo)
        if _oolX then
            for _OXlx, _lxlx in ipairs(_XXIX) do
                if _lxlx._oXxo == _oolX then return _lxlx end
            end
        end
        return nil
    end
    local _XXX = false
    local function _oxIO(_XIXO)
        if _XXX or not _OXOl then return end
        _XXX = true
        local _OOIO = _XIxX.offthread(buildOptions, 5)
        local _xOIx = _XIxX.try("main.refresh", function()
            if type(_OOIO) ~= "table" then
                _oloX.warn("refresh: egg read timed out - list left as it was")
                return
            end
            local _llxo = nil
            if _olo then
                for _xxIo, _OXXX in pairs(_lOX) do
                    if _OXXX == _olo then _llxo = _xxIo break end
                end
                if not _llxo then
                    _oloX._XIxo("selected egg %s is gone - clearing", tostring(_olo))
                    _olo = nil
                    if not (_Oooo.isRunning() and _Oooo._Xolo() == "main") then
                        _Oooo.setOptions("main", { _OXXX = nil })
                    end
                end
            end
            _OXOl:Refresh(_OOIO)
            if _llxo then _OXOl:Set(_llxo) end
        end)
        _XXX = false
        _oloX.trace("refresh (%s): %d options%s", tostring(_XIXO), #_XXIX,
            _xOIx and "" or " FAILED")
    end
    _xolx._oxIO = _oxIO
    function _xolx._XXxO(tab)
        if not tab then return _xolx end
        task.spawn(function() _IOo.setVisible(true) end)
        tab:CreateSection({ _oXxo = "How It Works" })
        tab:CreateText({
            _oXxo = "How It Works",
            _OllX = "Pick an egg and press Auto Steal. It baits the Forest "
                .. "guard, teleports to your egg, carries it to the safe zone "
                .. "and stops.",
        })
        tab:CreateSection({ _oXxo = "Target Egg" })
        tab:CreateText({
            _oXxo = "Target Browser",
            _OllX = "The Target UI shows the same ESP information inside the hub. "
                .. "Tap a card to select it and start Auto Steal immediately. "
                .. "Targets are ordered from best to worst by Gen/s.",
        })
        tab:CreateButton({
            _oXxo = "Open Target UI",
            callback = function()
                _IOo.setVisible(true)
            end,
        })
        tab:CreateSection({ _oXxo = "Auto Steal" })
        _lxXO = tab:CreateToggle({
            _oXxo = "Auto Steal",
            _XxOo = false,
            flag = "AutoSteal",
            callback = function(_IoIx)
                if _IoIx then
                    _oxX = 0      -- a real press clears any stale count
                    local _lOIO, _oxXX = _Oooo.setEnabled(true, "main")
                    if _lOIO == false then
                        _XxXX.notify("Auto Steal", tostring(_oxXX), 6)
                        task.spawn(function()
                            _XIxX.try("main.toggleRefused", function()
                                if _lxXO and _lxXO.Set then
                                    _oxX = _oxX + 1
                                    _lxXO:Set(false)
                                end
                            end)
                        end)
                    end
                    return
                end
                if _oxX > 0 then
                    _oxX = _oxX - 1
                    return
                end
                _Oooo.setEnabled(false, "main")
            end,
        })
        _Oooo.onIdle(function(_oxXX, _oIoo)
            if _oIoo and _oIoo ~= "main" then return end
            local _OllX = tostring(_oxXX)
            if _OllX:find("egg inventory full", 1, true) then
                _OllX = "Waiting: your egg inventory is full" .. (_OllX:match("%(%d+/%d+%)") and (" " .. _OllX:match("%(%d+/%d+%)")) or "")
                    .. ". Sell, place or hatch eggs - it starts by itself."
            elseif _OllX == "field resetting" then
                local _XIXo = _XIxX.require("core.data")
                local _IOxo = _XIXo.secondsUntilReset()
                local wait
                if _XIXo.fieldSealed() then
                    wait = (_IOxo and _IOxo < 60) and (_IOxo + 6) or 6
                else
                    wait = _IOxo and (_IOxo + 6) or nil
                end
                _OllX = wait and ("Waiting for the egg field reset - Auto Steal starts by itself in ~%ds. Leave it on."):format(math.ceil(wait))
                    or "Waiting for the egg field reset - Auto Steal starts by itself. Leave it on."
            else
                _OllX = "Waiting: " .. _OllX
            end
            task.spawn(function() _XxXX.notify("Auto Steal", _OllX, 7) end)
        end)
        _Oooo.onStop(function(_oxXX, _oIoo)
            if _oIoo and _oIoo ~= "main" then return end
            _Oooo.setOptions("main", { _OXXX = _olo, continuous = true })
            if _oxXX == "selected egg is gone" then
                task.spawn(function()
                    _XxXX.notify("Auto Steal", "Your egg is gone - stopped. Pick another.", 5)
                end)
            end
            task.spawn(function()
                _XIxX.try("main.toggleOff", function()
                    if _lxXO and _lxXO.Set then
                        _oxX = _oxX + 1
                        _lxXO:Set(false)
                    end
                end)
            end)
            if _oxXX == "delivered" then
                task.spawn(function()
                    _XxXX.notify("Auto Steal", "Delivered - stopped.", 4)
                end)
            end
        end)
        tab:CreateSection({ _oXxo = "ESP" })
        tab:CreateText({
            _oXxo = "Target ESP",
            _OllX = "Egg ESP cards are shown in the Target UI instead of being drawn over the map. "
                .. "The card keeps the image, name, Gen/s, KG and rarity.",
        })
        tab:CreateButton({
            _oXxo = "Show Target Cards",
            callback = function() _IOo.setVisible(true) end,
        })
        tab:CreateToggle({
            _oXxo = "Plot ESP",
            _XxOo = false,
            callback = function(_IoIx)
                _XIxX.try("main.plotEsp", function()
                    _XIxX.require("features.esp.plot").setEnabled(_IoIx)
                end)
            end,
        })
        tab:CreateSection({ _oXxo = "Anti Treadmill" })
        tab:CreateToggle({
            _oXxo = "Anti Treadmill",
            _XxOo = true,
            flag = "AntiTreadmill",
            callback = function(_IoIx)
                _lxOo.setEnabled(_IoIx and true or false)
            end,
        })
        local _lIlx = _XIxX.scope("ui.tabs.main")
        _lIlx:loop("prune", _OOOX._oIOo(10), function()
            if not _olo then return end
            local _loOo = _OOXo.get(_olo)
            if not _loOo then _oxIO("selected egg vanished") end
        end)
        _oloX._XIxo("main tab built (%d eggs)", #_XXIX)
        return _xolx
    end
    return _xolx
end)
_XIxX.module("ui.tabs.farm", function(_XIxX)
    local _Oooo   = _XIxX.require("features.autosteal")
    local _OOXo   = _XIxX.require("features.eggs")
    local _xxOO = _XIxX.require("features.farm.filter")
    local _oxXo   = _XIxX.require("features.farm.treadmill_on")
    local _llIX   = _XIxX.require("features.farm.pets")
    local _Xxoo   = _XIxX.require("features.farm.plotcare")
    local _XxXX    = _XIxX.require("ui.window")
    local _oloX    = _XIxX.require("boot.log").for_module("farm.tab")
    local _xolx = {}
    local _xXo, _OlX, _IIx
    local _olOl, _xoX
    local _xIXl, _oOX = nil, nil
    local function paintStatus(_OllX)
        if not _IIx or _OllX == _oOX then return end
        if _XIxX.try("farm.status", function() _IIx:Set(_OllX) end) then
            _oOX = _OllX
        end
    end
    local function statusText()
        local _xIlx = _xxOO._IXXO()
        if not _Oooo.isRunning() or _Oooo._Xolo() ~= "farm" then return "off" end
        local _oIxo = _Oooo._IXXO()._oIxo
        if _oIxo then
            local _xlOl = tostring(_oIxo):match("guards out: (.+)%)$")
            if _xlOl then
                return "ON  \u{B7}  waiting for the guard to walk home (" .. _xlOl .. ") - keeps going by itself"
            end
            return "ON  \u{B7}  waiting: " .. tostring(_oIxo)
        end
        if _Xxoo.isPlacing() and _Xxoo._IXXO():find("walking to your plot", 1, true) then
            return "ON  \u{B7}  placing the egg on your plot"
        end
        return "ON  \u{B7}  " .. tostring(_xIlx._OllX)
    end
    local _OIO = false
    local _oll = nil   -- a one-off line from a callback, painted next tick
    local _OXol, _OOol = nil, nil
    local function watchStatus(_IoIx)
        _OIO = _IoIx and true or false
    end
    local function watchPlot() end   -- the painter reads the switches itself
    local _xxol, _IIXl = 0, 0
    local _oXXl, _Illl = {}, {}
    local function labelsAndMap(_XXIX)
        local _lOoO, _xloX = {}, {}
        for _OXlx, _IlOx in ipairs(_XXIX) do
            _lOoO[#_lOoO + 1] = _IlOx._xxIo
            _xloX[_IlOx._xxIo] = _IlOx._OlIx
        end
        return _lOoO, _xloX
    end
    local function idsFor(_oxoO, _xloX)
        local _lxoX = {}
        if type(_oxoO) == "table" then
            for _OXlx, _xxIo in pairs(_oxoO) do
                local _OlIx = _xloX[tostring(_xxIo)]
                if _OlIx then _lxoX[#_lxoX + 1] = _OlIx end
            end
        elseif type(_oxoO) == "string" and _oxoO ~= "" then
            local _OlIx = _xloX[_oxoO]
            if _OlIx then _lxoX[#_lxoX + 1] = _OlIx end
        end
        return _lxoX
    end
    local function farmOptions()
        return {
            _OlIX = _xxOO._OlIX,
            continuous = true,
        }
    end
    function _xolx._XXxO(tab)
        if not tab then return _xolx end
        tab:CreateSection({ _oXxo = "How It Works" })
        tab:CreateText({
            _oXxo = "How It Works",
            _OllX = "Describe what you want and press Auto Steal. It keeps "
                .. "taking eggs that match until you turn it off. Main takes "
                .. "one egg you picked by name instead.",
        })
        tab:CreateSection({ _oXxo = "Egg Filters" })
        local _XlOl = _xxOO.areaOptions()
        local _oXo
        _oXo, _oXXl = labelsAndMap(_XlOl)
        _olOl = tab:CreateDropdown({
            _oXxo = "Areas",
            _OOIO = #_oXo > 0 and _oXo or { "No areas found" },
            multiSelect = true,
            flag = "FarmAreas",
            callback = function(_oxoO)
                _xxOO.setAreas(idsFor(_oxoO, _oXXl))
            end,
        })
        local _OXX = _xxOO.rarityOptions()
        local _xxl
        _xxl, _Illl = labelsAndMap(_OXX)
        _xoX = tab:CreateDropdown({
            _oXxo = "Rarities",
            _OOIO = #_xxl > 0 and _xxl or { "No rarities found" },
            multiSelect = true,
            flag = "FarmRarities",
            callback = function(_oxoO)
                _xxOO.setRarities(idsFor(_oxoO, _Illl))
            end,
        })
        tab:CreateDropdown({
            _oXxo = "Target By",
            _OOIO = _xxOO.targetByOptions(),
            currentOption = "Income",
            flag = "FarmTargetBy",
            callback = function(_XlOx)
                _xxOO.setTargetBy(type(_XlOx) == "table" and _XlOx[1] or _XlOx)
            end,
        })
        tab:CreateButton({
            _oXxo = "Refresh Eggs",
            callback = function()
                _OOXo.invalidate("farm refresh")
                _OOXo._OOxo({}, true)
                local _oIOx = _xxOO.matchCount()
                _oloX._XIxo("refresh: %d eggs match (%s)", _oIOx, _xxOO.describe())
                _XxXX.notify("Farm", _oIOx .. " eggs match your filters", 3)
                local _OXlx, _oxXX = _xxOO._OlIX()
                if not _OIO then
                    _oll = ("%d eggs match your filters%s"):format(_oIOx,
                        _oxXX and (_oIOx == 0) and ("  \u{B7}  " .. tostring(_xxOO._IXXO()._OllX)) or "")
                end
            end,
        })
        tab:CreateSection({ _oXxo = "Auto Farm" })
        _IIx = tab:CreateText({ _oXxo = "Status", _OllX = "off" })
        _xXo = tab:CreateToggle({
            _oXxo = "Auto Steal",
            _XxOo = false,
            flag = "FarmAutoSteal",
            callback = function(_IoIx)
                _XIxX.try("farm.autoToggle", function()
                    _oloX._XIxo("toggle -> %s", _IoIx and "ON" or "OFF")
                    if _IoIx then
                        _xxol = 0
                        if _oxXo.isOn() then _oxXo.setEnabled(false) end
                        _Oooo.setOptions("farm", farmOptions())
                        _oloX._XIxo("options handed over (%s)", _xxOO.describe())
                        local _lOIO, _oxXX = _Oooo.setEnabled(true, "farm")
                        _oloX._XIxo("start requested: running=%s owner=%s",
                            tostring(_Oooo.isRunning()), tostring(_Oooo._Xolo()))
                        if _lOIO == false then
                            _oll = tostring(_oxXX)
                            _XxXX.notify("Farm", tostring(_oxXX), 6)
                            task.spawn(function()
                                _XIxX.try("farm.toggleRefused", function()
                                    if _xXo and _xXo.Set then
                                        _xxol = _xxol + 1
                                        _xXo:Set(false)
                                    end
                                end)
                            end)
                            return
                        end
                        watchStatus(true)
                        return
                    end
                    watchStatus(false)
                    if _xxol > 0 then
                        _xxol = _xxol - 1
                        _oloX.trace("ignored our own Set(false)")
                        return
                    end
                    _Oooo.setEnabled(false, "farm")
                end)
            end,
        })
        _OlX = tab:CreateToggle({
            _oXxo = "Stay On Treadmill",
            _XxOo = false,
            flag = "StayOnTreadmill",
            callback = function(_IoIx)
                if _IIXl > 0 then
                    _IIXl = _IIXl - 1
                    return
                end
                local _xOIx, _oxXX = _oxXo.setEnabled(_IoIx and true or false)
                if _IoIx and not _xOIx then
                    _XIxX.try("farm.holdRefused", function()
                        if _OlX and _OlX.Set then
                            _IIXl = _IIXl + 1
                            _OlX:Set(false)
                        end
                    end)
                    _XxXX.notify("Farm", tostring(_oxXX or "Could not stay on the belt"), 4)
                end
            end,
        })
        tab:CreateSection({ _oXxo = "Plot" })
        _OXol = tab:CreateText({ _oXxo = "Plot", _OllX = _Xxoo._IXXO() })
        tab:CreateToggle({
            _oXxo = "Auto Place Eggs",
            _XxOo = false,
            callback = function(_IoIx)
                _XIxX.try("farm.autoPlace", function() _Xxoo.setPlace(_IoIx) end)
                watchPlot()
            end,
        })
        tab:CreateToggle({
            _oXxo = "Auto Hatch",
            _XxOo = false,
            callback = function(_IoIx)
                _XIxX.try("farm.autoHatch", function() _Xxoo.setHatch(_IoIx) end)
                watchPlot()
            end,
        })
        tab:CreateSection({ _oXxo = "Pets" })
        tab:CreateButton({
            _oXxo = "Equip Best Pets",
            callback = function()
                local _xOIx, _IooX = _llIX.equipBest()
                _XxXX.notify("Pets", tostring(_IooX), _xOIx and 3 or 4)
            end,
        })
        _xIXl = _XIxX.scope("ui.tabs.farm.paint")
        _xIXl:loop("paint", 1.0, function()
            if _OIO then
                _oll = nil
                paintStatus(statusText())
            elseif _oll then
                paintStatus(_oll)
                _oll = nil
            elseif _oOX and _oOX:find("^ON") and not _Oooo.isRunning() then
                paintStatus("off")
            end
            if _OXol then
                local _OllX = _Xxoo._IXXO()
                if _OllX ~= _OOol and _XIxX.try("farm.plotPaint", function() _OXol:Set(_OllX) end) then
                    _OOol = _OllX
                end
            end
        end)
        if not _xolx.wiredPlace then
            _xolx.wiredPlace = true
            _Oooo.setBetweenCycles(function(_oIoo)
                if _oIoo ~= "farm" or not _Xxoo.isPlacing() then return end
                _Xxoo.placeNow()
            end)
        end
        if not _xolx.wired then
            _xolx.wired = true
            _Oooo.onStop(function(_oxXX, _oIoo)
                if _oIoo and _oIoo ~= "farm" then return end
                task.spawn(function()
                    _XIxX.try("farm.toggleOff", function()
                        watchStatus(false)
                        if _xXo and _xXo.Set then
                            _xxol = _xxol + 1
                            _xXo:Set(false)
                        end
                    end)
                end)
            end)
        end
        _oloX._XIxo("farm tab built (%d areas, %d rarities)", #_oXo, #_xxl)
        return _xolx
    end
    function _xolx.teardown()
        _xXo, _OlX, _IIx, _olOl, _xoX = nil, nil, nil, nil, nil
        _oOX = nil
        if _xIXl then _xIXl:destroy() _xIXl = nil end
        if _Oooo.isRunning() and _Oooo._Xolo() == "farm" then _Oooo.setEnabled(false, "farm") end
        if _oxXo.isOn() then _oxXo.setEnabled(false) end
        _OXol, _OOol = nil, nil
        _OIO = false
        _Xxoo.setPlace(false)
        _Xxoo.setHatch(false)
        _oloX._XIxo("farm tab torn down")
    end
    return _xolx
end)
_XIxX.module("ui.tabs.event", function(_XIxX)
    local _Oxoo  = _XIxX.require("features.boss")
    local _OOIo = _XIxX.require("features.bossfight")
    local _lXIX  = _XIxX.require("features.rift")
    local _Oooo = _XIxX.require("features.autosteal")
    local _XxXX  = _XIxX.require("ui.window")
    local _oloX  = _XIxX.require("boot.log").for_module("event.tab")
    local _xolx = {}
    local _oolx = {
        PAINT = 1.0,
    }
    _xolx._oolx = _oolx
    local _lIlx = nil
    local _xOOl, _OlIl, _lxol, _ooIO, _OX, _oXO
    local _XIO, _xxol = 0, 0
    local _OOX = nil
    local _IoIO = {}      -- element -> { title =, body = } last written
    local function say(_IooX, _OxIX)
        _XxXX.notify("Event", tostring(_IooX), _OxIX or 3)
    end
    local function paint(_OxxX, _xIlx)
        if not _OxxX then return end
        local _xlxo = _IoIO[_OxxX]
        if not _xlxo then _xlxo = {} _IoIO[_OxxX] = _xlxo end
        if _xIlx._OXOo and _xIlx._OXOo ~= _xlxo._OXOo then
            if _XIxX.try("event.setTitle", function() _OxxX:SetTitle(_xIlx._OXOo) end) then
                _xlxo._OXOo = _xIlx._OXOo
            end
        end
        if _xIlx._Ixoo ~= _xlxo._Ixoo then
            if _XIxX.try("event.setBody", function() _OxxX:Set(_xIlx._Ixoo) end) then
                _xlxo._Ixoo = _xIlx._Ixoo
            end
        end
    end
    local function repaintBoss()
        paint(_xOOl, _Oxoo._IXXO())
        paint(_OlIl, _OOIo._IXXO())
    end
    local function repaintRift()
        paint(_lxol, _lXIX._IXXO())
        if not _ooIO then return end
        local _Xxxo = _lXIX._OOIO()
        local _lOXX = table.concat(_Xxxo, "\1")
        if _lOXX == _OOX then return end
        _OOX = _lOXX
        _XIxX.try("event.refreshDrop", function()
            _XIO = _XIO + 1
            _ooIO:Refresh(_Xxxo)
        end)
    end
    function _xolx._XXxO(tab)
        if not tab then return _xolx end
        tab:CreateSection({ _oXxo = "Boss" })
        _xOOl = tab:CreateText({ _oXxo = "Abyss Overlord", _OllX = "Reading..." })
        tab:CreateButton({
            _oXxo = "Enter the boss world",
            description = "Only works while it is open",
            callback = function()
                if not _Oxoo.isOn() then _Oxoo.setEnabled(true) end
                task.spawn(function()
                    _XIxX.try("event.enter", function()
                        local _xOIx, _oxXX = _Oxoo.enter()
                        say(_oxXX, _xOIx and 3 or 4)
                    end)
                end)
            end,
        })
        tab:CreateToggle({
            _oXxo = "Auto enter",
            description = "Joins as soon as it opens",
            _XxOo = false,
            callback = function(_XlOx)
                _XlOx = _XlOx and true or false
                if _XlOx and not _Oxoo.isOn() then _Oxoo.setEnabled(true) end
                _Oxoo.setAutoEnter(_XlOx)
                say("Auto enter " .. (_XlOx and "ON" or "OFF"))
            end,
        })
        _oXO = tab:CreateToggle({
            _oXxo = "Auto fight",
            description = "Breaks the crystals, then the boss",
            _XxOo = false,
            callback = function(_XlOx)
                _XlOx = _XlOx and true or false
                _OOIo.setEnabled(_XlOx)
                say("Auto fight " .. (_XlOx and "ON" or "OFF"))
            end,
        })
        _OlIl = tab:CreateText({ _oXxo = "Auto fight", _OllX = "off" })
        tab:CreateButton({
            _oXxo = "Claim mastery rewards",
            description = "Collects everything you have earned",
            callback = function()
                task.spawn(function()
                    _XIxX.try("event.claim", function()
                        local _oIOx, _IooX = _Oxoo.claimMilestones()
                        say(_IooX, _oIOx > 0 and 3 or 4)
                    end)
                end)
            end,
        })
        tab:CreateSection({ _oXxo = "Rift" })
        _lxol = tab:CreateText({ _oXxo = "Rift", _OllX = "reading..." })
        _ooIO = tab:CreateDropdown({
            _oXxo = "Rift pet",
            _OOIO = { _lXIX._oolx.NONE_LABEL },
            currentOption = _lXIX._oolx.NONE_LABEL,
            callback = function(_XlOx)
                if _XIO > 0 then
                    _XIO = _XIO - 1
                    _oloX.trace("ignored our own dropdown write")
                    return
                end
                if not _lXIX.isOn() then _lXIX.setEnabled(true) end
                local _oxoO = type(_XlOx) == "table" and _XlOx[1] or _XlOx
                local _OlIx = _lXIX.idForLabel(_oxoO)
                _lXIX.setPick(_OlIx)
                if _OlIx then say("Rift pet: " .. _lXIX.petName(_OlIx)) end
            end,
        })
        tab:CreateButton({
            _oXxo = "Refresh",
            description = "Re-read the rift and the pet list",
            callback = function()
                if not _lXIX.isOn() then _lXIX.setEnabled(true) end
                if not _Oxoo.isOn() then _Oxoo.setEnabled(true) end
                _Oxoo._oxIO()
                task.spawn(function()
                    _XIxX.try("event.riftRefresh", function()
                        _lXIX._oxIO("refresh button")
                        local _lxoX = _lXIX.onField()
                        if #_lxoX > 0 then
                            local _Xllo = {}
                            for _OXlx, _OlIx in ipairs(_lxoX) do _Xllo[#_Xllo+1] = _lXIX.petName(_OlIx) end
                            say("Rift: " .. table.concat(_Xllo, ", "), 4)
                        else
                            say("Rift: none out", 3)
                        end
                    end)
                end)
            end,
        })
        _OX = tab:CreateToggle({
            _oXxo = "Auto steal rift pets",
            description = "Steals only the rift pets",
            _XxOo = false,
            callback = function(_XlOx)
                if not _XlOx then
                    if _xxol > 0 then
                        _xxol = _xxol - 1
                        return
                    end
                    if _Oooo.isRunning() and _Oooo._Xolo() == "rift" then
                        _Oooo.setEnabled(false, "rift")
                    end
                    say("Rift auto OFF")
                    return
                end
                if not _lXIX.isOn() then _lXIX.setEnabled(true) end
                _Oooo.setOptions("rift", { _OlIX = _lXIX.pickTarget, continuous = true })
                _Oooo.setEnabled(true, "rift")
                say("Rift auto ON")
            end,
        })
        tab:CreateToggle({
            _oXxo = "Auto trade-in",
            description = "Puts your 3 rift pets in the Rift when you have them (lightest first, never equipped)",
            _XxOo = false,
            callback = function(_XlOx)
                _XlOx = _XlOx and true or false
                _lXIX.setAutoTrade(_XlOx)
                say("Auto trade-in " .. (_XlOx and "ON" or "OFF"))
            end,
        })
        if not _xolx.wired then
            _lXIX.onTrade(function(_IlOx)
                if not _lIlx then return end   -- torn down: premium has ended
                if _IlOx == "traded" then
                    say("Rift: traded in - Rift Egg added to your eggs", 5)
                elseif _IlOx ~= "revealed" then
                    say("Rift trade-in " .. tostring(_IlOx), 6)
                end
            end)
        end
        _lIlx = _XIxX.scope("ui.tabs.event")
        _lIlx:loop("paint", _oolx.PAINT, function()
            repaintBoss()
            repaintRift()
        end)
        _Oxoo.setEnabled(true)
        _lXIX.setEnabled(true)
        if not _xolx.wired then
            _xolx.wired = true
            _Oooo.onStop(function(_OXlx, _oIoo)
                if _oIoo and _oIoo ~= "rift" then return end
                task.spawn(function()
                    _XIxX.try("event.riftAutoOff", function()
                        if _OX and _OX.Set then
                            _xxol = _xxol + 1
                            _OX:Set(false)
                        end
                    end)
                end)
            end)
        end
        _oloX._XIxo("event tab built (V3.1 layout: Boss 5 + Rift 4; watchers on, painter %.0fs)", _oolx.PAINT)
        return _xolx
    end
    function _xolx.teardown()
        _xOOl, _OlIl, _lxol, _ooIO, _OX, _oXO = nil, nil, nil, nil, nil, nil
        _IoIO, _OOX, _XIO, _xxol = {}, nil, 0, 0
        if _lIlx then _lIlx:destroy() _lIlx = nil end
        _XIxX.try("event.teardown", function()
            if _Oooo.isRunning() and _Oooo._Xolo() == "rift" then _Oooo.setEnabled(false, "rift") end
            _OOIo.setEnabled(false)
            _Oxoo.setAutoEnter(false)
            _Oxoo.setEnabled(false)
            _lXIX.setAutoTrade(false)
            _lXIX.setEnabled(false)
        end)
        _oloX._XIxo("event tab torn down")
    end
    return _xolx
end)
_XIxX.module("ui.tabs.misc", function(_XIxX)
    local _IllO = _XIxX.require("features.misc.servers")
    local _xxXo    = _XIxX.require("features.misc.webhook")
    local _IXOX     = _XIxX.require("features.fps")
    local _XxXX     = _XIxX.require("ui.window")
    local _oloX     = _XIxX.require("boot.log").for_module("misc.tab")
    local _xolx = {}
    local _lOl = nil
    local function say(_OXOo, _xOIx, _IooX)
        _XxXX.notify(_OXOo, tostring(_IooX), _xOIx and 3 or 4)
    end
    function _xolx._XXxO(tab)
        if not tab then return _xolx end
        tab:CreateSection({ _oXxo = "Performance" })
        tab:CreateToggle({
            _oXxo = "FPS Boost",
            _XxOo = true,
            callback = function(_IoIx)
                _IoIx = _IoIx and true or false
                if not _IoIx then _IXOX.userTurnedOff = true end
                _XIxX.try("misc.fpsToggle", function() _IXOX.setEnabled(_IoIx) end)
            end,
        })
        tab:CreateSection({ _oXxo = "Servers" })
        tab:CreateButton({
            _oXxo = "Lowest Server",
            callback = function()
                local _xOIx, _IooX = _IllO.lowestServer()
                say("Servers", _xOIx, _IooX)
            end,
        })
        tab:CreateButton({
            _oXxo = "Server Hop",
            callback = function()
                local _xOIx, _IooX = _IllO.hop()
                say("Servers", _xOIx, _IooX)
            end,
        })
        tab:CreateSection({ _oXxo = "Webhooks" })
        local _oOXo = _XIxX.require("core.exec")
        tab:CreateToggle({
            _oXxo = "Enable Webhook",
            _XxOo = false,
            flag = "WebhookOn",
            callback = function(_IoIx)
                _XIxX.try("misc.webhookToggle", function() _xxXo.setEnabled(_IoIx) end)
                if _IoIx and not _oOXo.can._xxIO then
                    local _oxXX = "Webhooks are not supported by this executor (no HTTP request API)"
                    _oloX.warn("%s", _oxXX)
                    _XxXX.notify("Webhook", _oxXX, 6)
                    _XIxX.try("misc.webhookStatus", function()
                        if _lOl then _lOl:Set(_oxXX) end
                    end)
                end
            end,
        })
        if not _oOXo.can._xxIO then
            _lOl = tab:CreateText({
                _oXxo = "Webhook",
                _OllX = "Not supported by this executor (no HTTP request API). Everything else works.",
            })
        end
        tab:CreateInput({
            _oXxo = "Webhook URL",
            placeholder = "https://discord.com/api/webhooks/...",
            callback = function(_XlOx)
                local _xOIx, _IooX = _xxXo.setUrl(_XlOx)
                if not _xOIx then say("Webhooks", false, _IooX) end
            end,
        })
        tab:CreateButton({
            _oXxo = "Test Webhook",
            callback = function()
                local _xOIx, _IooX = _xxXo.test()
                say("Webhooks", _xOIx, _IooX)
            end,
        })
        _oloX._XIxo("misc tab built")
        return _xolx
    end
    function _xolx.teardown()
        _lOl = nil
        _XIxX.try("misc.teardown", function() _xxXo.setEnabled(false) end)
        _oloX._XIxo("misc tab torn down")
    end
    return _xolx
end)
_XIxX.module("ui.tabs.movement", function(_XIxX)
    local _olOo = _XIxX.require("features.speed")
    local _OOOX = _XIxX.require("core.device")
    local _XxXX = _XIxX.require("ui.window")
    local _oloX = _XIxX.require("boot.log").for_module("movement.tab")
    local _xolx = {}
    local _Xlo
    local _xO = 0
    local _lIlx = nil
    local _XOll, _lll = nil, nil
    local function paintSpeed()
        if not _XOll then return end
        local _OllX = _olOo._IXXO()
        if _OllX == _lll then return end
        if _XIxX.try("movement.speedPaint", function() _XOll:Set(_OllX) end) then
            _lll = _OllX
        end
    end
    function _xolx._XXxO(tab)
        if not tab then return _xolx end
        tab:CreateSection({ _oXxo = "How It Works" })
        tab:CreateText({
            _oXxo = "How It Works",
            _OllX = "Speed Boost makes your normal walking faster - you steer, it "
                .. "only adds speed. It pauses by itself while Auto Steal or Auto "
                .. "fight is moving you, and turns itself off if the server keeps "
                .. "correcting your movement.",
        })
        tab:CreateSection({ _oXxo = "Speed" })
        _XOll = tab:CreateText({ _oXxo = "Speed", _OllX = _olOo._IXXO() })
        _Xlo = tab:CreateToggle({
            _oXxo = "Speed Boost",
            _XxOo = false,
            callback = function(_IoIx)
                if not _IoIx and _xO > 0 then
                    _xO = _xO - 1
                    paintSpeed()
                    return
                end
                if _IoIx then _xO = 0 end
                _XIxX.try("movement.speedToggle", function() _olOo.setEnabled(_IoIx) end)
                paintSpeed()
            end,
        })
        if not _xolx.wired then
            _xolx.wired = true
            _olOo.onAutoOff(function(_oxXX) _XxXX.notify("Movement", tostring(_oxXX), 6) end)
        end
        _XIxX.try("movement.speedSlider", function()
            if type(tab.CreateSlider) ~= "function" then
                error("no CreateSlider on this build", 0)
            end
            tab:CreateSlider({
                _oXxo = "Walk Speed",
                range = { _olOo._oolx.SPEED_MIN, _olOo._oolx.SPEED_MAX },
                increment = 10,
                currentValue = _olOo._oolx.SPEED_DEFAULT,
                _oXXO = " studs/s",
                callback = function(_XlOx)
                    _olOo.setSpeed(_XlOx)
                    paintSpeed()
                end,
            })
        end)
        _lIlx = _XIxX.scope("ui.tabs.movement")
        _lIlx:loop("sync", _OOOX._oIOo(1.0), function()
            paintSpeed()
            if _Xlo and not _olOo.isOn() then
                local _llOo = _Xlo.CurrentValue
                if _llOo == nil then _llOo = _Xlo.Value end
                if _llOo == true then
                    _XIxX.try("movement.speedForceOff", function()
                        _xO = _xO + 1
                        _Xlo:Set(false)
                    end)
                end
            end
        end)
        _oloX._XIxo("movement tab built (touch=%s, fly removed)", tostring(_OOOX.isTouch))
        return _xolx
    end
    function _xolx.teardown()
        _Xlo, _xO = nil, 0
        _XOll, _lll = nil, nil
        if _lIlx then _lIlx:destroy() _lIlx = nil end
        _XIxX.try("movement.speedTeardown", function() _olOo.setEnabled(false) end)
        _oloX._XIxo("movement tab torn down")
    end
    return _xolx
end)
_XIxX.module("ui.tabs.config", function(_XIxX)
    local _XOIX = _XIxX.require("core.profiles")
    local _XOxo = _XIxX.require("features.misc.appearance")
    local _XxXX  = _XIxX.require("ui.window")
    local _oloX  = _XIxX.require("boot.log").for_module("config.tab")
    local _xolx = {}
    local _XlIO, _xOol, _lOOl, _lxXl, _IIx
    local _oloo = "None"
    local function say(_xOIx, _IooX)
        _XxXX.notify("Config", tostring(_IooX), _xOIx and 3 or 4)
        _XIxX.try("config.status", function()
            if _IIx then _IIx:Set(tostring(_IooX)) end
        end)
    end
    local function _OOIO()
        local _OOxo = _XOIX._OOxo()
        local _lxoX = { _oloo }
        for _OXlx, _oIOx in ipairs(_OOxo) do _lxoX[#_lxoX + 1] = _oIOx end
        return _lxoX
    end
    local function refreshLists()
        local _Xxxo = _OOIO()
        _XIxX.try("config.refreshLists", function()
            if _xOol and _xOol.Refresh then _xOol:Refresh(_Xxxo) end
            if _lOOl and _lOOl.Refresh then _lOOl:Refresh(_Xxxo) end
        end)
        return _Xxxo
    end
    local function boxValue(_XIOX)
        if not _XIOX then return "" end
        local _XlOx = _XIOX.CurrentValue
        if _XlOx == nil or _XlOx == "" then _XlOx = _XIOX.Value end
        if _XlOx == nil or _XlOx == "" then _XlOx = _XIOX._XxOo end
        if (_XlOx == nil or _XlOx == "") and typeof(_XIOX._oxIo) == "Instance" then
            pcall(function() _XlOx = _XIOX._oxIo.Text end)
        end
        return tostring(_XlOx or "")
    end
    local function _OlIX(_XlOx)
        local _llOx = type(_XlOx) == "table" and _XlOx[1] or _XlOx
        _llOx = tostring(_llOx or "")
        if _llOx == _oloo then return "" end
        return _llOx
    end
    function _xolx._XXxO(tab)
        if not tab then return _xolx end
        tab:CreateSection({ _oXxo = "Appearance" })
        tab:CreateDropdown({
            _oXxo = "Theme",
            _OOIO = _XOxo.themes(),
            flag = "Theme",
            callback = function(_XlOx)
                local _xOIx, _IooX = _XOxo.setTheme(_OlIX(_XlOx))
                if not _xOIx then say(false, _IooX) end
            end,
        })
        _lxXl = tab:CreateInput({
            _oXxo = "Background Image ID",
            placeholder = "0000000000",
            flag = "Background",
            callback = function(_XlOx)
                local _xOIx, _IooX = _XOxo.setBackground(_XlOx)
                say(_xOIx, _IooX)
            end,
        })
        tab:CreateButton({
            _oXxo = "Clear Background",
            callback = function()
                local _xOIx, _IooX = _XOxo.clearBackground()
                _XIxX.try("config.clearInput", function()
                    if _lxXl and _lxXl.Set then _lxXl:Set("") end
                end)
                say(_xOIx, _IooX)
            end,
        })
        tab:CreateSection({ _oXxo = "Profiles" })
        if not _XOIX.available() then
            tab:CreateText({
                _oXxo = "Profiles",
                _OllX = "Config saving is not supported by this executor. "
                    .. "Everything else works normally.",
            })
            _oloX.warn("no filesystem (%s) - profile controls not built",
                table.concat(_XIxX.require("core.exec").report()._OlIO, ","))
            return _xolx
        end
        _XlIO = tab:CreateInput({
            _oXxo = "Profile Name",
            placeholder = "my settings",
            callback = function() end,
        })
        _IIx = tab:CreateText({ _oXxo = "Status", _OllX = "Type a name and press Save Profile" })
        tab:CreateButton({
            _oXxo = "Save Profile",
            callback = function()
                local _xOIx, _IooX = _XOIX._lxIX(boxValue(_XlIO))
                if _xOIx then refreshLists() end
                say(_xOIx, _IooX)
            end,
        })
        _xOol = tab:CreateDropdown({
            _oXxo = "Load Profile",
            _OOIO = _OOIO(),
            currentOption = _oloo,
            callback = function(_XlOx)
                local _oXxo = _OlIX(_XlOx)
                if _oXxo == "" then return end
                local _xOIx, _IooX = _XOIX.load(_oXxo)
                say(_xOIx, _IooX)
            end,
        })
        tab:CreateButton({
            _oXxo = "Refresh Profiles",
            callback = function()
                _XOIX._oxIO()
                local _Xxxo = refreshLists()
                say(true, (#_Xxxo - 1) .. " profiles")
            end,
        })
        tab:CreateButton({
            _oXxo = "Delete Profile",
            callback = function()
                local _xOIx, _IooX = _XOIX.delete(boxValue(_XlIO))
                if _xOIx then refreshLists() end
                say(_xOIx, _IooX)
            end,
        })
        _lOOl = tab:CreateDropdown({
            _oXxo = "Auto Load Profile",
            _OOIO = _OOIO(),
            currentOption = _XOIX.autoLoadName() or _oloo,
            callback = function(_XlOx)
                local _xOIx, _IooX = _XOIX.setAutoLoad(_OlIX(_XlOx))
                say(_xOIx, _IooX)
            end,
        })
        _oloX._XIxo("config tab built (%d profiles)", #_XOIX._OOxo())
        return _xolx
    end
    return _xolx
end)
_XIxX.module("features.movement", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _lXxX  = _XIxX.require("core.character")
    local _OOOX = _XIxX.require("core.device")
    local _xxIx  = _XIxX.require("core.restore")
    local _oloX = _XIxX.require("boot.log").for_module("movement")
    local RunService, Players = _OoXX.RunService, _OoXX.Players
    local _xolx = {}
    local _oolx = {
        GROUND_OFFSET     = 3,
        CRUISE_UP         = 18,    -- studs above the higher end to cruise at
        RAMP_FRAC         = 0.12,  -- share of flat distance spent climbing/diving
        RAMP_MAX          = 220,
        RAMP_MIN          = 40,    -- less than this and the climb is a vertical jerk
        START_SPEED       = 0.45,  -- fraction of cruise we leave the ground at
        SPEED_RAMP_FRAC   = 0.28,
        SLOW_RADIUS       = 50,    -- careful approach inside this
        SLOW_SPEED        = 260,
        ARRIVE            = 5,
        MAX_DT            = 0.05,  -- longest SINGLE write, in seconds
        MAX_FRAME         = 0.25,  -- most travel repaid in one frame
        MAX_DEBT          = 2.0,   -- most unspent time carried forward
        MAX_STEP          = 20,    -- ceiling on one write's displacement
        SPEED             = 1200,  -- outbound cruise ceiling
        SPEED_NOSPOOF     = 500,   -- measured safe without a spoof
        NOSPOOF_FLOOR     = 300,
        NOSPOOF_CONVERGE  = 40,
        DROP_SPEED        = 400,
        SPOOF_HEADROOM    = 1.35,  -- claimed WalkSpeed = speed * this
        WS_MAX            = 4000,
        WALKSPEED_SANE_MIN = 40,
        RELOC_CLAMP_FOR   = 6,
        RELOC_CLAMP_RATIO = 1.04,
        TP_SETTLE         = 0.35,
        TP_LANDED         = 30,
    }
    _xolx._oolx = _oolx
    local _IOxX = nil
    function _xolx.setAnticheat(adapter) _IOxX = adapter end
    local function acGet(_oXxo)
        local _Oxlx = _IOxX and _IOxX[_oXxo]
        return type(_Oxlx) == "function" and _Oxlx or nil
    end
    local _xXl = RaycastParams._oooX()
    _xXl.FilterType = Enum.RaycastFilterType.Exclude
    _xXl.IgnoreWater = true
    local _XXO = true
    local _xll = {}   -- reused; never reallocated per call
    local function rebuildFilter()
        local _oIOx = 0
        for _xxlx = #_xll, 1, -1 do _xll[_xxlx] = nil end
        for _OXlx, pl in ipairs(Players:GetPlayers()) do
            if pl.Character then
                _oIOx = _oIOx + 1
                _xll[_oIOx] = pl.Character
            end
        end
        _xXl.FilterDescendantsInstances = _xll
        _XXO = false
    end
    local function solidGroundY(_IIXX)
        if _XXO then rebuildFilter() end
        local _oXoO = _IIXX + Vector3._oooX(0, 80, 0)
        local _oOOX = Vector3._oooX(0, -700, 0)
        local _IOIo = nil
        for _OXlx = 1, 15 do
            local _IlOx = workspace:Raycast(_oXoO, _oOOX, _xXl)
            if not _IlOx then break end
            if _IlOx.Instance.CanCollide then
                if _IOIo then _xXl.FilterDescendantsInstances = _xll end
                return _IlOx.Position.Y + _oolx.GROUND_OFFSET
            end
            _IOIo = _IOIo or table._OIIo(_xll)
            _IOIo[#_IOIo + 1] = _IlOx.Instance
            _xXl.FilterDescendantsInstances = _IOIo
        end
        if _IOIo then _xXl.FilterDescendantsInstances = _xll end
        return nil
    end
    local function groundOr(_IIXX, _IIol)
        return solidGroundY(_IIXX) or _IIol
    end
    _xolx.groundY = solidGroundY
    local _oool, _XxIl, _xxO, _oxIl = nil, nil, nil, nil
    local function noclipStep()
        local _xxoo = _lXxX.get()
        if not _xxoo then return end
        if _oxIl ~= _xxoo or not _xxO then
            _xxO, _oxIl, _XxIl = {}, _xxoo, {}
            for _OXlx, _xIOx in ipairs(_xxoo:GetDescendants()) do
                if _xIOx:IsA("BasePart") then
                    _xxO[#_xxO + 1] = _xIOx
                    _XxIl[_xIOx] = _xIOx.CanCollide
                end
            end
        end
        for _xxlx = 1, #_xxO do
            local _xIOx = _xxO[_xxlx]
            if _xIOx.Parent and _xIOx.CanCollide then _xIOx.CanCollide = false end
        end
    end
    function _xolx.noclip(_IoIx)
        if _IoIx then
            if _oool then return end
            _xxIx.onRestore("movement.noclip", function() _xolx.noclip(false) end)
            _oool = _XIxX.scope("features.movement.noclip")
            _oool:onFrame("noclip", RunService.Stepped, noclipStep)
        else
            if not _oool then return end
            _oool:destroy()
            _oool = nil
            if _XxIl then
                for _XIIX, _lxXX in pairs(_XxIl) do
                    if _XIIX.Parent then pcall(function() _XIIX.CanCollide = _lxXX end) end
                end
            end
            _xxO, _XxIl, _oxIl = nil, nil, nil
        end
    end
    local _xIOX = { _XloX = nil, high = nil, _olOo = nil, legSpeed = nil, legRelocs = nil }
    function _xolx.outboundSpeed()
        return _oolx.SPEED
    end
    function _xolx.carrySpeedCap()
        if not acGet("relocateCount") then return _oolx.SPEED_NOSPOOF end
        return _xIOX._olOo or _oolx.SPEED_NOSPOOF
    end
    local function bracketAfterLeg()
        local _xIIo = acGet("relocateCount")
        if not _xIIo or not _xIOX.legSpeed then return end
        local _IolX = _xIOX.legSpeed
        local _XOIl = _xIIo() > (_xIOX.legRelocs or 0)
        if _XOIl then
            _xIOX.high = _IolX                                   -- too fast
        else
            _xIOX._XloX = math._IOoX(_xIOX._XloX or _oolx.SPEED_NOSPOOF, _IolX)
        end
        local _XloX = _xIOX._XloX or _oolx.SPEED_NOSPOOF
        local _OxIl
        if _xIOX.high then
            if (_xIOX.high - _XloX) <= _oolx.NOSPOOF_CONVERGE then
                _OxIl = _XloX                               -- settled at the safe max
            else
                _OxIl = math.floor((_XloX + _xIOX.high) / 2)
            end
        else
            _OxIl = math.min(_oolx.SPEED, _XloX * 2)
        end
        _OxIl = math.clamp(_OxIl, _oolx.NOSPOOF_FLOOR, _oolx.SPEED)
        if _OxIl ~= (_xIOX._olOo or _oolx.SPEED_NOSPOOF) then
            _oloX._XIxo("travel: %s at %d - next leg %d studs/s (bracket %d..%s)",
                _XOIl and "relocated" or "clean", _IolX, _OxIl,
                _XloX, tostring(_xIOX.high or "-"))
        end
        _xIOX._olOo = _OxIl
        _xIOX.legSpeed = nil
    end
    local _xOOo = { legs = 0, _oxx = 0, respawned = 0, timedOut = 0, _XXXl = 0,
                    teleports = 0, tpLanded = 0, tpRefused = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.teleport(_IIXX, _ooXX)
        local _xxoo, _XxOX = _lXxX.get(), _lXxX._oXIX()
        if not _xxoo or not _XxOX then return false, math.huge end
        local _IIIx = solidGroundY(_IIXX)
        local _OlXo = Vector3._oooX(_IIXX.X, _IIIx or _IIXX.Y, _IIXX.Z)
        local _ooXo = _XxOX.Position
        local _xOIx = pcall(function() _xxoo:PivotTo(CFrame._oooX(_OlXo)) end)
        if _xOIx then
            _XxOX.AssemblyLinearVelocity = Vector3.zero
            _XxOX.AssemblyAngularVelocity = Vector3.zero
        end
        task.wait(_OOOX._oIOo(_oolx.TP_SETTLE))
        local _lIIx = _lXxX._oXIX()
        local _lXOX = _lIIx and (_lIIx.Position - _OlXo).Magnitude or math.huge
        local _OOoO = _lXOX <= _oolx.TP_LANDED
        _xOOo.teleports = _xOOo.teleports + 1
        if _OOoO then
            _xOOo.tpLanded = _xOOo.tpLanded + 1
        else
            _xOOo.tpRefused = _xOOo.tpRefused + 1
        end
        _oloX._XIxo("tp %s: %.0f studs -> %s (%.0f off, tier=%s)",
            tostring(_ooXX), (_OlXo - _ooXo).Magnitude,
            _OOoO and "landed" or "REFUSED", _lXOX, _OOOX.tier)
        return _OOoO, _lXOX
    end
    local function writeStep(_xxoo, _IIoX, _XxOX, _OlXo, _XOxo)
        if _IIoX then _IIoX:Move(Vector3.zero, false) end
        _xxoo:PivotTo(CFrame.lookAt(_OlXo, _OlXo + _XOxo))
        _XxOX.AssemblyLinearVelocity = Vector3.zero
        _XxOX.AssemblyAngularVelocity = Vector3.zero
    end
    function _xolx.travel(_Xxxo)
        local _IIXX      = _Xxxo._Xllx
        local _ooXX      = _Xxxo._ooXX or "leg"
        local _xIOO   = _Xxxo._xIOO or _oolx.ARRIVE
        local _OoOl = _Xxxo._OoOl and true or false
        local _IoOO   = _Xxxo._IoOO
        local _xxoo = _lXxX.get()
        local _XxOX  = _lXxX._oXIX()
        local _IIoX  = _lXxX.humanoid()
        if not _xxoo or not _XxOX then
            _oloX.warn("%s: no character to move", _ooXX)
            return false, { _XIXO = "no-character" }
        end
        local _olOo = math._IOoX(_Xxxo._olOo or _oolx.SPEED_NOSPOOF, 40)
        local _oOOo = _XxOX.Position
        local _XlIl = Vector3._oooX(_IIXX.X - _oOOo.X, 0, _IIXX.Z - _oOOo.Z).Magnitude
        if _XlIl < 1 then return true, { _XIXO = "already-there", _IXOl = 0 } end
        local _xlo = groundOr(_oOOo, _oOOo.Y)
        local _XIIl   = groundOr(_IIXX, _IIXX.Y)
        local _IIlo   = _XIIl
        local _OIxl = math._IOoX(_xlo, _XIIl, _oOOo.Y, _IIXX.Y) + _oolx.CRUISE_UP
        local _OoIX = math.clamp(_XlIl * _oolx.RAMP_FRAC, _oolx.RAMP_MIN, _oolx.RAMP_MAX)
        if _OoIX * 2 > _XlIl * 0.9 then _OoIX = _XlIl * 0.45 end
        if _XlIl < _oolx.RAMP_MIN * 2 then _OIxl = math._IOoX(_oOOo.Y, _IIXX.Y) end
        local _IIoo = _IIoX and _IIoX.PlatformStand or false
        if _IIoX then
            _xxIx.remember("movement.platformStand",
                function() return _IIoX.PlatformStand end,
                function(_XlOx) _IIoX.PlatformStand = _XlOx end)
            _IIoX.PlatformStand = true
        end
        local _IoIX, _XllO = acGet("push"), acGet("spoof")
        local _XlOo = (not _OoOl) and _IIoX and true or false
        local _xxXl, _oIlO = nil, nil
        if _XlOo then
            _xxIx.remember("movement.walkSpeed",
                function() return _IIoX.WalkSpeed end,
                function(_XlOx) _IIoX.WalkSpeed = _XlOx end)
            _oIlO = _IIoX.WalkSpeed
            _xxXl = math.clamp(_olOo * _oolx.SPOOF_HEADROOM, 16, _oolx.WS_MAX)
            _IIoX.WalkSpeed = _xxXl
        end
        if not _OoOl and not _XlOo then
            _xIOX.legSpeed = _olOo
            local _xIIo = acGet("relocateCount")
            _xIOX.legRelocs = _xIIo and _xIIo() or 0
        end
        local _OIlo = _loIx.clock()
        local _Ollx = _OIlo
        local _XoOl = _Ollx + math._IOoX(_XlIl / _olOo, 0.3) * 3 + 6
        local _lIlo = _Ollx
        local _OXXl = 0
        local _xOIx, _XIXO = false, "timeout"
        local _lIoO, _oIO, _Oxl = 0, 0, 0
        _oloX.trace("%s: begin %.0f studs at %.0f studs/s (carrying=%s spoof=%s tier=%s)",
            _ooXX, _XlIl, _olOo, tostring(_OoOl), tostring(_XlOo), _OOOX.tier)
        while _loIx.clock() < _XoOl do
            if _IoOO and _IoOO() then _XIXO = "cancelled" break end
            local _XOol = _lXxX.get()
            if _XOol ~= _xxoo then
                _XIXO = "respawned"
                break
            end
            local _OIIx = _lXxX._oXIX()
            if not _OIIx then _XIXO = "lost-root" break end
            local _XooX = _loIx.clock()
            local _oIXX = _XooX - _lIlo
            _lIlo = _XooX
            _OXXl = math.min(_OXXl + _oIXX, _oolx.MAX_DEBT)
            local _Ooxl = math.min(_OXXl, _oolx.MAX_FRAME)
            _OXXl = _OXXl - _Ooxl
            if _oIXX > _Oxl then _Oxl = _oIXX end
            local _IlXl = math._IOoX(1, math.ceil(_Ooxl / _oolx.MAX_DT))
            local _xXxX = _Ooxl / _IlXl
            _lIoO = _lIoO + 1
            _oIO = _oIO + _IlXl
            local _IoXo = Vector3._oooX(_IIXX.X - _OIIx.Position.X, 0, _IIXX.Z - _OIIx.Position.Z)
            local _IlXX = _IoXo.Magnitude
            if _IlXX <= _xIOO then _xOIx, _XIXO = true, "arrived" break end
            local _IOXo = math._IOoX(_XlIl - _IlXX, 0)
            local _oolX
            local _xOll = math._IOoX(_OoIX * _oolx.SPEED_RAMP_FRAC, 1)
            if _IlXX <= _oolx.SLOW_RADIUS then
                _oolX = math.min(_oolx.SLOW_SPEED, _olOo)
            elseif _IlXX < _OoIX then
                local _Oxlx = _IlXX / _OoIX
                _oolX = math._IOoX(_olOo * _Oxlx, math.min(_oolx.SLOW_SPEED, _olOo))
            elseif _IOXo < _xOll then
                _oolX = _olOo * (_oolx.START_SPEED + (1 - _oolx.START_SPEED) * (_IOXo / _xOll))
            else
                _oolX = _olOo
            end
            local _OXIl = acGet("lastRelocateAt")
            local _XxIO = _OXIl and _OXIl() or nil
            if _XxIO and (not _OoOl or _XxIO >= _OIlo)
               and (_loIx.clock() - _XxIO) < _oolx.RELOC_CLAMP_FOR then
                local _XoXl = acGet("allowance")
                local _XOxO = _XoXl and _XoXl() or nil
                if not _XOxO and _IIoX and _IIoX.WalkSpeed > _oolx.WALKSPEED_SANE_MIN then
                    _XOxO = _IIoX.WalkSpeed * _oolx.RELOC_CLAMP_RATIO
                end
                if _XOxO and _XOxO > 0 and _oolX > _XOxO then
                    _oolX = _XOxO
                end
            end
            local _xxOo
            if _OoOl then
                -- Durante o transporte do egg, mantém o personagem no chão
                -- em vez de seguir a "arc" elevada que fazia ele flutuar.
                _xxOo = _IIlo
            elseif _IOXo < _OoIX then
                _xxOo = _oOOo.Y + (_OIxl - _oOOo.Y) * (_IOXo / _OoIX)
            elseif _IlXX < _OoIX then
                _xxOo = _IIlo + (_OIxl - _IIlo) * (_IlXX / _OoIX)
            else
                _xxOo = _OIxl
            end
            local _XXXl = false
            for _OXlx = 1, _IlXl do
                local _XIIx = _OIIx.Position
                local _XxxX = Vector3._oooX(_IIXX.X - _XIIx.X, 0, _IIXX.Z - _XIIx.Z)
                local _xoIX = _XxxX.Magnitude
                if _xoIX <= _xIOO then _XXXl = true break end
                local _lool = _OoOl and (_oolX * _l) or _oolX
                local _oIlX = math.min(_xoIX, _lool * _xXxX, _oolx.MAX_STEP)
                local _xOlX = _XxxX.Unit
                local _xooX = _XIIx + _xOlX * _oIlX

                if _OoOl then
                    -- Recalcula o chão ao longo do caminho para acompanhar
                    -- rampas/terreno irregular sem deixar o personagem no ar.
                    local _IIIx = groundOr(Vector3._oooX(_xooX.X, _XIIx.Y, _xooX.Z), _IIlo)
                    pcall(writeStep, _xxoo, _IIoX, _OIIx,
                        Vector3._oooX(_xooX.X, _IIIx, _xooX.Z), _xOlX)
                else
                    pcall(writeStep, _xxoo, _IIoX, _OIIx,
                        Vector3._oooX(_xooX.X, _xxOo, _xooX.Z), _xOlX)
                end
            end
            if _XXXl then _xOIx, _XIXO = true, "arrived" break end
            if _XlOo then
                if _IIoX.WalkSpeed < _xxXl - 1 then _IIoX.WalkSpeed = _xxXl end
                if _IoIX or _XllO then
                    local _IOlX = _IoXo.Unit * math.min(_oolX, _xxXl)
                    if _IoIX then _IoIX(_OIIx, _IIoX, _IOlX) else _XllO(_xxXl, _IOlX) end
                end
                pcall(function() _OIIx.AssemblyLinearVelocity = Vector3.zero end)
            end
            RunService.Heartbeat:Wait()
        end
        local _llIx = _lXxX._oXIX()
        local _XOol = _lXxX.get()
        if _llIx and _XOol == _xxoo then
            local _IIIx = solidGroundY(_llIx.Position)
            if _IIIx and math.abs(_llIx.Position.Y - _IIIx) > 1 then
                pcall(function() _xxoo:PivotTo(CFrame._oooX(_llIx.Position.X, _IIIx, _llIx.Position.Z)) end)
            end
        end
        if _XlOo and _IIoX and _IIoX.Parent then
            local _IlIO = acGet("legalWalkSpeed")
            local _oIlo = _IlIO and _IlIO() or _oIlO or 16
            pcall(function() _IIoX.WalkSpeed = math._IOoX(_oIlo, 16) end)
        end
        if _IIoX and _IIoX.Parent then
            _IIoX.PlatformStand = _IIoo
            local _lloO = _IIoX:GetState()
            if _lloO == Enum.HumanoidStateType.Freefall
               or _lloO == Enum.HumanoidStateType.PlatformStanding
               or _lloO == Enum.HumanoidStateType.Physics then
                pcall(function() _IIoX:ChangeState(Enum.HumanoidStateType.Landed) end)
            end
        end
        if _llIx then
            _llIx.AssemblyLinearVelocity = Vector3.zero
            _llIx.AssemblyAngularVelocity = Vector3.zero
        end
        if not _OoOl and not _XlOo then bracketAfterLeg() end
        local _lXOX = _llIx and Vector3._oooX(_IIXX.X - _llIx.Position.X, 0, _IIXX.Z - _llIx.Position.Z).Magnitude
            or math.huge
        local _Olxl = _loIx.clock() - _Ollx
        local _lllO = _xOIx or _lXOX <= _xIOO + 4
        _xOOo.legs = _xOOo.legs + 1
        _xOOo[_lllO and "arrived" or (_XIXO == "cancelled" and "cancelled")
            or (_XIXO == "respawned" and "respawned") or "timedOut"] =
            (_xOOo[_lllO and "arrived" or (_XIXO == "cancelled" and "cancelled")
            or (_XIXO == "respawned" and "respawned") or "timedOut"] or 0) + 1
        local _XIlo = _lllO and _oloX.trace or _oloX.warn
        _XIlo("%s: %s %.0f studs in %.2fs (want %.0f/s, %.0f/s actual, %.1f short) "
            .. "reason=%s frames=%d sub=%.1f worstFrame=%.0fms tier=%s",
            _ooXX, _lllO and "ok" or "FAILED", _XlIl, _Olxl, _olOo,
            _XlIl / math._IOoX(_Olxl, 0.001), _lXOX, _XIXO, _lIoO,
            _lIoO > 0 and (_oIO / _lIoO) or 0,
            _Oxl * 1000, _OOOX.tier)
        return _lllO, {
            _XIXO = _XIXO, _IXOl = _XlIl, _Olxl = _Olxl,
            _lXOX = _lXOX, _lIoO = _lIoO, worstFrameMs = _Oxl * 1000,
        }
    end
    function _xolx.descend(_ooXX)
        _ooXX = _ooXX or "land"
        local _xxoo, _Xxlx = _lXxX.get(), _lXxX._oXIX()
        if not _xxoo or not _Xxlx then return false end
        local _IIoX = _lXxX.humanoid()
        local _IIIx = solidGroundY(_Xxlx.Position)
        if not _IIIx then
            if _IIoX then _IIoX.PlatformStand = false end
            _oloX.trace("%s: no ground below - falling", _ooXX)
            return false
        end
        local _IOOx, _OOOx = _Xxlx.Position.X, _Xxlx.Position.Z
        local _ooXo = _Xxlx.Position.Y
        if _ooXo - _IIIx <= 2 then
            if _IIoX then _IIoX.PlatformStand = false end
            return true
        end
        if _IIoX then _IIoX.PlatformStand = true end
        local _Ollx = _loIx.clock()
        local _XOOX = math.clamp((_ooXo - _IIIx) / math._IOoX(_oolx.DROP_SPEED, 50), 0.05, 1.2)
        while _loIx.clock() - _Ollx < _XOOX do
            if _lXxX.get() ~= _xxoo then break end
            local _OIIx = _lXxX._oXIX()
            if not _OIIx then break end
            local _Oxlx = (_loIx.clock() - _Ollx) / _XOOX
            local _lOOx = _ooXo + (_IIIx - _ooXo) * _Oxlx
            pcall(function()
                _xxoo:PivotTo(CFrame._oooX(_IOOx, _lOOx, _OOOx) * (_OIIx.CFrame - _OIIx.CFrame.Position))
                _OIIx.AssemblyLinearVelocity = Vector3.zero
            end)
            RunService.Heartbeat:Wait()
        end
        if _lXxX.get() == _xxoo then
            pcall(function() _xxoo:PivotTo(CFrame._oooX(_IOOx, _IIIx, _OOOx)) end)
        end
        if _IIoX and _IIoX.Parent then
            _IIoX.PlatformStand = false
            pcall(function() _IIoX:ChangeState(Enum.HumanoidStateType.Landed) end)
        end
        _oloX.trace("%s: descended %.0f studs to ground", _ooXX, _ooXo - _IIIx)
        return true
    end
    local _lIlx = _XIxX.scope("features.movement")
    _lIlx:connect(Players.PlayerAdded, function() _XXO = true end)
    _lIlx:connect(Players.PlayerRemoving, function() _XXO = true end)
    _lXxX.onSpawn(_lIlx, "movement.respawn", function()
        _XXO = true
        _xxO, _XxIl, _oxIl = nil, nil, nil
    end)
    function _xolx.reset()
        _xolx.noclip(false)
    end
    return _xolx
end)
_XIxX.module("features.speed", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _lXxX   = _XIxX.require("core.character")
    local _xIlx   = _XIxX.require("core.state")
    local _XlOX  = _XIxX.require("core.config")
    local _XIXo = _XIxX.require("core.data")
    local _XooO = _XIxX.require("core.motion")
    local _oloX  = _XIxX.require("boot.log").for_module("speed")
    local _xolx = {}
    local _oolx = {
        SPEED_DEFAULT = 300,
        SPEED_MIN     = 20,     -- with the slider's 10-stud step, values land round
        SPEED_MAX     = 1000,   -- the fastest measured clean; above it is untested
        FORCE         = 1e7,
        DEADZONE      = 0.05,   -- MoveDirection below this is "no input"
        COOLDOWN      = 3.0,
        STRIKES       = 3,
        STRIKE_WINDOW = 30,
        SNAP_MIN      = 30,     -- studs in one frame that no boost explains
    }
    _xolx._oolx = _oolx
    local _lIlx, _olxl = nil, false
    local _olOo = _oolx.SPEED_DEFAULT
    local _OIOX, _lOIx = nil, nil
    local _OoOl = false
    local _Ioll = nil      -- why the boost is idle right now, or nil
    local _lIIl, _IOlO = 0, {}
    local _xXx = 0        -- last frame the constraint was pushing
    local _oIIO = nil
    local _XXo = nil
    local _xl = {}
    local _xOOo = { enables = 0, _lIoO = 0, respawns = 0, corrections = 0, autoOffs = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    function _xolx._olOo() return _olOo end
    function _xolx.onAutoOff(_xxxX) _xl[#_xl + 1] = _xxxX end
    function _xolx.setSpeed(_oIOx)
        _oIOx = tonumber(_oIOx)
        if not _oIOx then return false, "not a number" end
        _olOo = math.clamp(math.floor(_oIOx), _oolx.SPEED_MIN, _oolx.SPEED_MAX)
        _oloX._XIxo("speed %d studs/s", _olOo)
        return true, _olOo
    end
    local _Ooo = { autosteal = "Auto Steal is running", bossfight = "Auto fight is moving you",
                         _oxXo = "holding the treadmill", _ooOX = "Fly is on" }
    local function _XxXl()
        local _OOxO = _XooO._XXx("speed")
        if _OOxO then return _Ooo[_OOxO] or (_OOxO .. " is moving you") end
        if _loIx.clock() < _lIIl then return "server corrected your movement - cooling down" end
        if _xIlx.autoStealOn then return "Auto Steal is running" end
        if _xIlx.stayOnTreadmill then return "holding the treadmill" end
        local _ooOX = _XIxX._loaded["features.fly"]
        if _ooOX and _ooOX.isOn() then return "Fly is on" end
        local _OOIo = _XIxX._loaded["features.bossfight"]
        local _IOIx = _OoXX.Players.LocalPlayer
        if _OOIo and _OOIo.isOn() and _IOIx and _IOIx:GetAttribute("InBossArena") == true then
            return "Auto fight is in the arena"
        end
        return nil
    end
    local function detach()
        if _lOIx then pcall(function() _lOIx:Destroy() end) end
        if _OIOX then pcall(function() _OIOX:Destroy() end) end
        _OIOX, _lOIx = nil, nil
    end
    local function attach(_oXIX)
        detach()
        if not (_oXIX and _oXIX:IsA("BasePart")) then return false end
        _OIOX = Instance._oooX("Attachment")
        _OIOX.Name = "RyuzakiSpeedAtt"
        _lOIx = Instance._oooX("LinearVelocity")
        _lOIx.Name = "RyuzakiSpeed"
        _lOIx.Attachment0 = _OIOX
        _lOIx.MaxForce = _oolx.FORCE
        _lOIx.RelativeTo = Enum.ActuatorRelativeTo.World
        _lOIx.VelocityConstraintMode = Enum.VelocityConstraintMode.Plane
        _lOIx.PrimaryTangentAxis = Vector3._oooX(1, 0, 0)
        _lOIx.SecondaryTangentAxis = Vector3._oooX(0, 0, 1)
        _lOIx.Enabled = false
        _lIlx:own(_OIOX)
        _lIlx:own(_lOIx)
        _OIOX.Parent = _oXIX
        _lOIx.Parent = _oXIX
        return true
    end
    local function _oIlX()
        if not _lOIx then return end
        _xOOo._lIoO = _xOOo._lIoO + 1
        local _oxXX = _XxXl()
        if _oxXX ~= _Ioll then
            _Ioll = _oxXX
            if _oxXX then _oloX._XIxo("standing down: %s", _oxXX) end
        end
        if _oxXX then
            if _lOIx.Enabled then _lOIx.Enabled = false end
            _oIIO = nil      -- another owner may teleport us; not a snap
            return
        end
        local _IIoX = _lXxX.humanoid()     -- live: the Humanoid can be swapped under us
        local _oXIX = _lXxX._oXIX()
        if not _IIoX or not _oXIX or _IIoX.Health <= 0 or _lOIx.Parent ~= _oXIX then
            if _lOIx.Enabled then _lOIx.Enabled = false end
            _oIIO = nil
            return
        end
        local _IIXX = _oXIX.Position
        if _oIIO and _lOIx.Enabled then
            local _XIol = math._IOoX(_olOo * 0.1, _oolx.SNAP_MIN)
            if (_IIXX - _oIIO).Magnitude > _XIol then
                _oIIO = _IIXX
                _xolx.corrected("snap")
                return
            end
        end
        _oIIO = _IIXX
        local _oOOX = _IIoX.MoveDirection
        if _oOOX.Magnitude < _oolx.DEADZONE then
            local _XlOx = _oXIX.AssemblyLinearVelocity
            local _IoXo = Vector3._oooX(_XlOx.X, 0, _XlOx.Z).Magnitude
            if _IoXo > (_IIoX.WalkSpeed + 5) then
                _lOIx.PlaneVelocity = Vector2.zero
                if not _lOIx.Enabled then _lOIx.Enabled = true end
            elseif _lOIx.Enabled then
                _lOIx.Enabled = false
            end
            return
        end
        local _XlOx = _olOo
        if _OoOl then
            _XlOx = math.min(_XlOx, (tonumber(_XlOX.CARRY_SPEED) or 500) * 0.9)
        end
        local _olOx = _oOOX.Unit
        _lOIx.PlaneVelocity = Vector2._oooX(_olOx.X * _XlOx, _olOx.Z * _XlOx)
        if not _lOIx.Enabled then _lOIx.Enabled = true end
        _xXx = _loIx.clock()
    end
    function _xolx.corrected(_Xlxo)
        if not _olxl or not _lOIx then return end
        local _XooX = _loIx.clock()
        if (_XooX - _xXx) > 0.6 then return end
        _xOOo.corrections = _xOOo.corrections + 1
        _lOIx.Enabled = false
        _XIxX.try("speed.cutMomentum", function()
            local _oXIX = _lXxX._oXIX()
            if _oXIX then
                local _XlOx = _oXIX.AssemblyLinearVelocity
                _oXIX.AssemblyLinearVelocity = Vector3._oooX(0, math.min(_XlOx.Y, 0), 0)
            end
        end)
        _lIIl = _XooX + _oolx.COOLDOWN
        for _xxlx = #_IOlO, 1, -1 do
            if _XooX - _IOlO[_xxlx] > _oolx.STRIKE_WINDOW then table.remove(_IOlO, _xxlx) end
        end
        _IOlO[#_IOlO + 1] = _XooX
        _oloX.warn("server corrected the boost (%s) at %d studs/s - strike %d/%d, pausing %.0fs",
            tostring(_Xlxo), _olOo, #_IOlO, _oolx.STRIKES, _oolx.COOLDOWN)
        if #_IOlO >= _oolx.STRIKES then
            _XXo = ("the server corrected your movement %d times - Speed Boost turned off"):format(#_IOlO)
            _xOOo.autoOffs = _xOOo.autoOffs + 1
            _oloX.warn("%s", _XXo)
            task.spawn(function()
                _xolx.setEnabled(false)
                for _OXlx, _xxxX in ipairs(_xl) do _XIxX.try("speed.onAutoOff", _xxxX, _XXo) end
            end)
        end
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        if not _IoIx then
            _olxl = false
            _XooO.release("speed")
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            _oIIO, _IOlO, _lIIl = nil, {}, 0
            _XIxX.try("speed.offBrake", function()
                local _oXIX = _lXxX._oXIX()
                if _oXIX then
                    local _XlOx = _oXIX.AssemblyLinearVelocity
                    _oXIX.AssemblyLinearVelocity = Vector3._oooX(0, _XlOx.Y, 0)
                end
            end)
            _OIOX, _lOIx, _Ioll = nil, nil, nil
            _oloX._XIxo("off")
            return true
        end
        _olxl = true
        _XXo = nil
        _xOOo.enables = _xOOo.enables + 1
        _lIlx = _XIxX.scope("features.speed")
        _XooO.claim("speed")
        _XooO.onRejected(_lIlx, function(_Xlxo) _xolx.corrected(_Xlxo) end)
        _XIxX.try("speed.carryWatch", function()
            local _xIxX = _XIXo.eggState()
            if _xIxX and _xIxX.CarryChanged then
                _lIlx:connect(_xIxX.CarryChanged, function(_XIxo)
                    _OoOl = type(_XIxo) == "table" and _XIxo.IsCarrying == true
                end)
            end
        end)
        _XIxX.try("speed.carryNow", function()
            _OoOl = _XIxX.require("features.eggs").carryingUid() ~= nil
        end)
        _lXxX.onSpawn(_lIlx, "speed.respawn", function(_xxoo)
            _xOOo.respawns = _xOOo.respawns + 1
            local _oXIX = _xxoo and _xxoo:WaitForChild("HumanoidRootPart", 5)
            attach(_oXIX)
        end)
        local _XOlo, _lIXX = pcall(function() return _OoXX.RunService.PreSimulation end)
        local _xOXO = (_XOlo and _lIXX) or _OoXX.RunService.Heartbeat
        _lIlx:onFrame("step", _xOXO, _oIlX)
        _oloX._XIxo("on (%d studs/s)", _olOo)
        return true
    end
    _XIxX.onTeardown("speed", function() _xolx.setEnabled(false) end)
    function _xolx._IXXO()
        if not _olxl then return _XXo and ("off  \u{B7}  " .. _XXo) or "off" end
        if _Ioll then return "paused: " .. _Ioll end
        return ("on  \u{B7}  %d studs/s"):format(_olOo)
    end
    return _xolx
end)
_XIxX.module("features.humanoid", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _lXxX  = _XIxX.require("core.character")
    local _xxIx  = _XIxX.require("core.restore")
    local _oloX = _XIxX.require("boot.log").for_module("humanoid")
    local _xolx = {}
    local _lox = "RyuzakiStealHum"
    _xolx._lox = _lox
    local _lIlx = nil
    local _Xoll = nil
    local _xOOo = { swaps = 0, alreadySwapped = 0, _xxOl = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isSwapped()
        local _IIoX = _lXxX.humanoid()
        return _IIoX ~= nil and _IIoX:GetAttribute(_lox) == true
    end
    local function applyStates(_Ixlo)
        local _IIoX = _lXxX.humanoid()
        if not _IIoX or _IIoX:GetAttribute(_lox) ~= true then return end
        _IIoX:SetStateEnabled(Enum.HumanoidStateType.Dead, _Ixlo._xIXo)
        _IIoX:SetStateEnabled(Enum.HumanoidStateType.FallingDown, _Ixlo.fallingDown)
        _IIoX:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, _Ixlo.ragdoll)
        _IIoX.BreakJointsOnDeath = _Ixlo.breakJoints
    end
    local function rememberStates(_Ixlo)
        _xxIx.remember("humanoid.states",
            function() return _Ixlo end,
            function(_XlOx) applyStates(_XlOx) end)
    end
    function _xolx.swap(_xxoo)
        _xxoo = _xxoo or _lXxX.get()
        if not _xxoo then return false end
        local _IIoX = _xxoo:FindFirstChildOfClass("Humanoid")
        if not _IIoX then return false end
        if _IIoX:GetAttribute(_lox) == true then
            _xOOo.alreadySwapped = _xOOo.alreadySwapped + 1
            if not _Xoll then
                local _Ixlx = _IIoX:GetAttribute("RyuzakiPriorDead")
                if _Ixlx ~= nil then
                    _Xoll = {
                        _xIXo        = _Ixlx,
                        fallingDown = _IIoX:GetAttribute("RyuzakiPriorFallingDown") ~= false,
                        ragdoll     = _IIoX:GetAttribute("RyuzakiPriorRagdoll") ~= false,
                        breakJoints = _IIoX:GetAttribute("RyuzakiPriorBreakJoints") == true,
                    }
                    rememberStates(_Xoll)
                end
            end
            _XIxX.try("humanoid.reapply", function()
                _IIoX.BreakJointsOnDeath = false
                _IIoX:SetStateEnabled(Enum.HumanoidStateType.Dead, false)
                _IIoX:SetStateEnabled(Enum.HumanoidStateType.FallingDown, false)
                _IIoX:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, false)
            end)
            return true
        end
        local _Ixlo = {
            _xIXo        = _IIoX:GetStateEnabled(Enum.HumanoidStateType.Dead),
            fallingDown = _IIoX:GetStateEnabled(Enum.HumanoidStateType.FallingDown),
            ragdoll     = _IIoX:GetStateEnabled(Enum.HumanoidStateType.Ragdoll),
            breakJoints = _IIoX.BreakJointsOnDeath,
        }
        local _xOIx = _XIxX.try("humanoid.swap", function()
            local _Ixl = _xxoo:FindFirstChild("Health")
            if _Ixl then _Ixl:Destroy() end
            _IIoX.BreakJointsOnDeath = false
            _IIoX.Archivable = true
            local _OIIo = _IIoX:Clone()
            if not _OIIo then error("clone failed") end
            _OIIo.Name = "Humanoid"
            _OIIo:SetAttribute(_lox, true)
            _OIIo:SetAttribute("RyuzakiPriorDead", _Ixlo._xIXo)
            _OIIo:SetAttribute("RyuzakiPriorFallingDown", _Ixlo.fallingDown)
            _OIIo:SetAttribute("RyuzakiPriorRagdoll", _Ixlo.ragdoll)
            _OIIo:SetAttribute("RyuzakiPriorBreakJoints", _Ixlo.breakJoints)
            _OIIo:SetStateEnabled(Enum.HumanoidStateType.Dead, false)
            _OIIo:SetStateEnabled(Enum.HumanoidStateType.FallingDown, false)
            _OIIo:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, false)
            _OIIo.Health = _IIoX.MaxHealth
            if not _OIIo:FindFirstChildOfClass("Animator") then
                Instance._oooX("Animator").Parent = _OIIo
            end
            _IIoX:Destroy()
            _OIIo.Parent = _xxoo
            if workspace.CurrentCamera then
                workspace.CurrentCamera.CameraSubject = _OIIo
            end
            local _xoXl = _xxoo:FindFirstChild("Animate")
            if _xoXl then
                local _IOxX = _xoXl:Clone()
                _xoXl:Destroy()
                _IOxX.Parent = _xxoo
                _IOxX.Disabled = false
            end
            for _OXlx, _Ixlx in ipairs(_xxoo:GetDescendants()) do
                if _Ixlx:IsA("Motor6D") then _Ixlx.Enabled = true end
            end
        end)
        if _xOIx then
            _xxIx.permanent("humanoid.swap",
                "Humanoid replaced and Health script destroyed - undone by respawn")
            _Xoll = _Ixlo
            rememberStates(_Ixlo)
            _xOOo.swaps = _xOOo.swaps + 1
            _oloX._XIxo("swapped (anticheat now holds a destroyed Humanoid)")
        else
            _xOOo._xxOl = _xOOo._xxOl + 1
            _oloX.error("swap FAILED - teleports will be punished")
        end
        return _xOIx and true or false
    end
    function _xolx.isArmed() return _lIlx ~= nil end
    function _xolx.arm()
        if _lIlx then return true end
        _lIlx = _XIxX.scope("features.humanoid")
        _xolx.swap()
        _lXxX.onSpawn(_lIlx, "humanoid.reswap", function(_xxoo)
            _Xoll = nil
            _xolx.swap(_xxoo)
        end)
        return true
    end
    function _xolx.disarm()
        if not _Xoll then
            local _IIoX = _lXxX.humanoid()
            if _IIoX and _IIoX:GetAttribute(_lox) == true then
                local _Ixlx = _IIoX:GetAttribute("RyuzakiPriorDead")
                _Xoll = {
                    _xIXo        = (_Ixlx == nil) and true or _Ixlx,
                    fallingDown = _IIoX:GetAttribute("RyuzakiPriorFallingDown") ~= false,
                    ragdoll     = _IIoX:GetAttribute("RyuzakiPriorRagdoll") ~= false,
                    breakJoints = _IIoX:GetAttribute("RyuzakiPriorBreakJoints") == true,
                }
            end
        end
        if _Xoll then
            _XIxX.try("humanoid.restoreStates", function()
                applyStates(_Xoll)
                _oloX._XIxo("death states restored (dead=%s fallingDown=%s "
                    .. "ragdoll=%s breakJoints=%s) - the character can respawn "
                    .. "normally again",
                    tostring(_Xoll._xIXo), tostring(_Xoll.fallingDown),
                    tostring(_Xoll.ragdoll), tostring(_Xoll.breakJoints))
            end)
        end
        if not _lIlx then return end
        _lIlx:destroy()
        _lIlx = nil
        _oloX._XIxo("disarmed (%d swaps this session)", _xOOo.swaps)
    end
    return _xolx
end)
_XIxX.module("features.jump", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _lXxX   = _XIxX.require("core.character")
    local _xIlx   = _XIxX.require("core.state")
    local _xxOX  = _XIxX.require("features.humanoid")
    local _oloX  = _XIxX.require("boot.log").for_module("jump")
    local _xolx = {}
    local _lIlx = nil
    local _xOOo = { requests = 0, _lXXl = 0, duringRun = 0, unswapped = 0, busy = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isArmed() return _lIlx ~= nil end
    function _xolx.arm()
        if _lIlx then return true end
        _lIlx = _XIxX.scope("features.jump")
        _lIlx:connect(_OoXX.UserInputService.JumpRequest, function()
            _xOOo.requests = _xOOo.requests + 1
            if _xIlx.autoStealOn then
                _xOOo.duringRun = _xOOo.duringRun + 1
                return
            end
            local _IIoX = _lXxX.humanoid()
            if not _IIoX then return end
            if _IIoX:GetAttribute(_xxOX._lox) ~= true then
                _xOOo.unswapped = _xOOo.unswapped + 1
                return
            end
            if _IIoX.Health <= 0 then return end
            local _XOOo = _IIoX:GetState()
            if _XOOo == Enum.HumanoidStateType.Jumping
               or _XOOo == Enum.HumanoidStateType.Freefall then
                _xOOo.busy = _xOOo.busy + 1
                return
            end
            _IIoX.Jump = true
            _xOOo._lXXl = _xOOo._lXXl + 1
        end)
        _oloX._XIxo("armed - the player's jump reaches the live humanoid")
        return true
    end
    function _xolx.disarm()
        if not _lIlx then return end
        _lIlx:destroy()
        _lIlx = nil
        _oloX._XIxo("disarmed (%d requests, %d applied)", _xOOo.requests, _xOOo._lXXl)
    end
    return _xolx
end)
_XIxX.module("features.antideath", function(_XIxX)
    local _lXxX  = _XIxX.require("core.character")
    local _OoXX = _XIxX.require("core.services")
    local _xxIx  = _XIxX.require("core.restore")
    local _oloX = _XIxX.require("boot.log").for_module("antideath")
    local _xolx = {}
    local _lIlx = nil
    local _OIOo = nil        -- the values we must put back
    local _IOOl = nil     -- which Humanoid the current arming belongs to
    local _xOOo = { arms = 0, deathsBlocked = 0, restores = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    local function applyTo(_xxoo)
        local _IIoX = _xxoo and _xxoo:FindFirstChildOfClass("Humanoid")
        if not _IIoX then return false end
        if _IOOl == _IIoX then return true end
        _OIOo = {
            humanoid = _IIoX,
            breakJoints = _IIoX.BreakJointsOnDeath,
            deadEnabled = _IIoX:GetStateEnabled(Enum.HumanoidStateType.Dead),
        }
        _IOOl = _IIoX
        _XIxX.try("antideath.apply", function()
            _xxIx.remember("antideath.breakJoints",
                function() return _IIoX.BreakJointsOnDeath end,
                function(_XlOx) _IIoX.BreakJointsOnDeath = _XlOx end)
            _xxIx.remember("antideath.state.Dead",
                function() return _IIoX:GetStateEnabled(Enum.HumanoidStateType.Dead) end,
                function(_XlOx) _IIoX:SetStateEnabled(Enum.HumanoidStateType.Dead, _XlOx) end)
            _IIoX.BreakJointsOnDeath = false
            _IIoX:SetStateEnabled(Enum.HumanoidStateType.Dead, false)
        end)
        _lIlx:connect(_IIoX.HealthChanged, function(_XIIx)
            if _XIIx <= 0 and _IIoX.Parent then
                _xOOo.deathsBlocked = _xOOo.deathsBlocked + 1
                _IIoX.Health = _IIoX.MaxHealth
            end
        end)
        _lIlx:connect(_IIoX.StateChanged, function(_OXlx, _oooX)
            if _oooX == Enum.HumanoidStateType.Dead and _IIoX.Parent then
                _xOOo.deathsBlocked = _xOOo.deathsBlocked + 1
                _IIoX:ChangeState(Enum.HumanoidStateType.GettingUp)
                _IIoX.Health = _IIoX.MaxHealth
            end
        end)
        if _IIoX.Health <= 0 then
            _xOOo.deathsBlocked = _xOOo.deathsBlocked + 1
            _oloX.warn("armed on a humanoid already at 0 health - reviving it")
            _IIoX.Health = _IIoX.MaxHealth
        end
        _xOOo.arms = _xOOo.arms + 1
        _oloX.trace("armed on humanoid (health %.0f/%.0f)", _IIoX.Health, _IIoX.MaxHealth)
        return true
    end
    local function restore()
        local _llOx = _OIOo
        _OIOo, _IOOl = nil, nil
        if not _llOx or not _llOx.humanoid or not _llOx.humanoid.Parent then return end
        _xOOo.restores = _xOOo.restores + 1
        _XIxX.try("antideath.restore", function()
            _llOx.humanoid.BreakJointsOnDeath = _llOx.breakJoints
            _llOx.humanoid:SetStateEnabled(Enum.HumanoidStateType.Dead, _llOx.deadEnabled)
        end)
    end
    function _xolx.isArmed() return _lIlx ~= nil end
    function _xolx.arm()
        if _lIlx then return true end
        _lIlx = _XIxX.scope("features.antideath")
        local _xOIx = applyTo(_lXxX.get())
        _lXxX.onSpawn(_lIlx, "antideath.rearm", function(_xxoo)
            _OIOo, _IOOl = nil, nil
            applyTo(_xxoo)
        end)
        _oloX._XIxo("armed (%s)", _xOIx and "ok" or "no humanoid yet")
        return true
    end
    function _xolx.disarm()
        if not _lIlx then return end
        _lIlx:destroy()
        _lIlx = nil
        _XIxX.try("antideath.reviveOnDisarm", function()
            local _IIoX = _lXxX.humanoid()
            if _IIoX and _IIoX.Parent and _IIoX.Health <= 0 then
                _oloX.warn("disarming on 0 health - reviving before restoring states")
                _IIoX.Health = _IIoX.MaxHealth
            end
        end)
        restore()
        _oloX._XIxo("disarmed (blocked %d deaths this session)", _xOOo.deathsBlocked)
    end
    return _xolx
end)
_XIxX.module("features.guard", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _XIXo = _XIxX.require("core.data")
    local _lXxX  = _XIxX.require("core.character")
    local _xxIx  = _XIxX.require("core.restore")
    local _oloX = _XIxX.require("boot.log").for_module("guard")
    local RunService = _OoXX.RunService
    local _xolx = {}
    local _oolx = {
        RISE      = 150,   -- upward studs/s no legal jump can produce
        FLAT_MULT = 2.5,   -- flat speed over WalkSpeed * this is not our doing
        FLAT_MIN  = 150,   -- ...but never react below this, whatever WalkSpeed is
        JOINT_GAP = 0.25,  -- seconds between Motor6D sweeps; they are not free
        HOLD_MAX  = 2.75,  -- longest we wait out the server knockdown
        HOLD_GRACE = 0.25, -- covers the release round trip
    }
    _xolx._oolx = _oolx
    local _lIlx = nil
    local _xOOo = { launchesCancelled = 0, standUps = 0, dropsRefused = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isRagdolled()
        local _IIoX = _lXxX.humanoid()
        if not _IIoX then return false end
        if _IIoX.PlatformStand then return true end
        local _llOx = _IIoX:GetState()
        return _llOx == Enum.HumanoidStateType.Physics
            or _llOx == Enum.HumanoidStateType.Ragdoll
            or _llOx == Enum.HumanoidStateType.FallingDown
    end
    function _xolx.waitForRecovery(_xIlO)
        local _XoOl = _loIx.clock() + (_xIlO or 4)
        while _loIx.clock() < _XoOl do
            if not _xolx.isRagdolled() then return true end
            RunService.Heartbeat:Wait()
        end
        return false
    end
    local function applyAntiRagdoll(_xxoo)
        _xxoo = _xxoo or _lXxX.get()
        local _IIoX = _xxoo and _xxoo:FindFirstChildOfClass("Humanoid")
        if not _IIoX then return false end
        _XIxX.try("guard.antiRagdoll", function()
            _xxIx.remember("guard.state.Ragdoll",
                function() return _IIoX:GetStateEnabled(Enum.HumanoidStateType.Ragdoll) end,
                function(_XlOx) _IIoX:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, _XlOx) end)
            _xxIx.remember("guard.state.FallingDown",
                function() return _IIoX:GetStateEnabled(Enum.HumanoidStateType.FallingDown) end,
                function(_XlOx) _IIoX:SetStateEnabled(Enum.HumanoidStateType.FallingDown, _XlOx) end)
            _IIoX:SetStateEnabled(Enum.HumanoidStateType.Ragdoll, false)
            _IIoX:SetStateEnabled(Enum.HumanoidStateType.FallingDown, false)
            for _OXlx, _Ixlx in ipairs(_xxoo:GetDescendants()) do
                if _Ixlx:IsA("Motor6D") then _Ixlx.Enabled = true end
            end
        end)
        return true
    end
    local _lXl, _IIl, _xoO = nil, false, nil
    local _XoO = false
    local function installDropBlock()
        if _IIl then return true end
        _xoO = _xoO or _XIXo.eggState()
        if not _xoO or type(_xoO.DropFieldEgg) ~= "function" then
            _oloX.warn("cannot block egg drops - EggState.DropFieldEgg missing")
            return false
        end
        _lXl = _xoO.DropFieldEgg
        _xoO.DropFieldEgg = function(_XIXO, ...)
            if not _XoO then
                _xOOo.dropsRefused = _xOOo.dropsRefused + 1
                _oloX.trace("drop refused: %s", tostring(_XIXO))
                return
            end
            return _lXl(_XIXO, ...)
        end
        _IIl = true
        _oloX._XIxo("egg-drop block installed")
        return true
    end
    local function removeDropBlock()
        if not _IIl then return end
        _XIxX.try("guard.restoreDrop", function()
            if _xoO and _lXl then
                _xoO.DropFieldEgg = _lXl
            end
        end)
        _IIl, _lXl = false, nil
    end
    function _xolx.allowDrops(_IoIx) _XoO = _IoIx and true or false end
    local _oxXl, _oXXX, _lIIO = 0, 0, 0
    local function antiHitStep()
        local _IIoX, _XxOX = _lXxX.humanoid(), _lXxX._oXIX()
        if not _IIoX or not _XxOX then return end
        local _xIlx = _IIoX:GetState()
        if _xIlx == Enum.HumanoidStateType.Jumping then return end
        local _XlOx = _XxOX.AssemblyLinearVelocity
        local _IoXo = (_XlOx * Vector3._oooX(1, 0, 1)).Magnitude
        local _XOxl = math._IOoX((_IIoX.WalkSpeed or 16) * _oolx.FLAT_MULT, _oolx.FLAT_MIN)
        if _XlOx.Y > _oolx.RISE or _IoXo > _XOxl then
            local _llxo = Vector3.zero
            if _IoXo > 0.001 then
                _llxo = (_XlOx * Vector3._oooX(1, 0, 1)).Unit * math.min(_IoXo, _IIoX.WalkSpeed or 16)
            end
            _XxOX.AssemblyLinearVelocity = Vector3._oooX(_llxo.X, math.min(_XlOx.Y, 0), _llxo.Z)
            _XxOX.AssemblyAngularVelocity = Vector3.zero
            _oxXl = _oxXl + 1
            _xOOo.launchesCancelled = _oxXl
        end
        if _IIoX.PlatformStand or _IIoX.Sit
           or _xIlx == Enum.HumanoidStateType.Physics
           or _xIlx == Enum.HumanoidStateType.Ragdoll
           or _xIlx == Enum.HumanoidStateType.FallingDown
           or _xIlx == Enum.HumanoidStateType.PlatformStanding then
            pcall(function()
                _IIoX.PlatformStand = false
                _IIoX.Sit = false
                _IIoX:ChangeState(Enum.HumanoidStateType.GettingUp)
            end)
            _oXXX = _oXXX + 1
            _xOOo.standUps = _oXXX
            local _XooX = _loIx.clock()
            if _XooX - _lIIO > _oolx.JOINT_GAP then
                _lIIO = _XooX
                local _xxoo = _lXxX.get()
                if _xxoo then
                    for _OXlx, _Ixlx in ipairs(_xxoo:GetDescendants()) do
                        if _Ixlx:IsA("Motor6D") and not _Ixlx.Enabled then _Ixlx.Enabled = true end
                    end
                end
            end
        end
    end
    function _xolx.ragdollRemaining()
        local _IOxo = 0
        _XIxX.try("guard.ragdollRemaining", function()
            local _oxoX = _OoXX.LocalPlayer
            local _OlOx = _oxoX and _oxoX:GetAttribute("RagdollEndTime")
            if type(_OlOx) == "number" then
                _IOxo = math._IOoX(_IOxo, _OlOx - workspace:GetServerTimeNow())
            end
        end)
        return math._IOoX(0, _IOxo)
    end
    function _xolx.waitForServerRelease(_IoOO)
        local _lxXo = _xolx.ragdollRemaining()
        if _lxXo <= 0 then return 0 end
        local _Ollx = _loIx.clock()
        local _XoOl = _loIx.clock() + math.min(_lxXo, _oolx.HOLD_MAX)
        while _loIx.clock() < _XoOl do
            if _IoOO and _IoOO() then break end
            task.wait(0.05)
            if _xolx.ragdollRemaining() <= 0 then break end
        end
        task.wait(_oolx.HOLD_GRACE)
        local _xxXO = _loIx.clock() - _Ollx
        _oloX.trace("server held us %.2fs - waited %.2fs", _lxXo, _xxXO)
        return _xxXO
    end
    function _xolx.isArmed() return _lIlx ~= nil end
    function _xolx.arm()
        if _lIlx then return true end
        _lIlx = _XIxX.scope("features.guard")
        _oxXl, _oXXX, _lIIO = 0, 0, 0
        _XoO = false
        applyAntiRagdoll()
        installDropBlock()
        _lIlx:onFrame("antihit", RunService.Heartbeat, antiHitStep)
        _lXxX.onSpawn(_lIlx, "guard.respawn", function(_xxoo)
            applyAntiRagdoll(_xxoo)
        end)
        _oloX._XIxo("armed (anti-hit + anti-ragdoll + drop block)")
        return true
    end
    function _xolx.disarm()
        if not _lIlx then return end
        _lIlx:destroy()
        _lIlx = nil
        _XoO = true
        removeDropBlock()
        _oloX._XIxo("disarmed (%d launches cancelled, %d stand-ups, %d drops refused)",
            _xOOo.launchesCancelled, _xOOo.standUps, _xOOo.dropsRefused)
    end
    return _xolx
end)
_XIxX.module("features.guardwatch", function(_XIxX)
    local _lOIX = _XIxX.require("features.plot")
    local _oloX  = _XIxX.require("boot.log").for_module("guardwatch")
    local _xolx = {}
    local _oolx = {
        BEHIND_OK = 60,
    }
    _xolx._oolx = _oolx
    local _OOXl = { Sleeping = true, Waking = true }
    local _xOOo = { checks = 0, _oxXl = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    local function guardOf(_oIOO)
        local _oxlx
        pcall(function() _oxlx = workspace.__OBJECTS.Areas.GuardAreas[_oIOO].Guard end)
        return _oxlx
    end
    local function rootOf(_oxlx)
        local _IlOx = _oxlx and (_oxlx:FindFirstChild("HumanoidRootPart") or _oxlx.PrimaryPart)
        return (_IlOx and _IlOx:IsA("BasePart")) and _IlOx or nil
    end
    function _xolx.blocking(_oIOO, nestPos)
        _xOOo.checks = _xOOo.checks + 1
        if not _oIOO or typeof(nestPos) ~= "Vector3" then return nil end
        local _oxlx = guardOf(_oIOO)
        local _oXIX = rootOf(_oxlx)
        if not _oXIX then return nil end
        local _XOOo = tostring(_oxlx:GetAttribute("GuardState") or "")
        if _OOXl[_XOOo] then return nil end
        local _XxXo = _lOIX.safeZone()
        if typeof(_XxXo) ~= "Vector3" then return nil end
        local _lIOo = (_XxXo - nestPos) * Vector3._oooX(1, 0, 1)
        if _lIOo.Magnitude < 1 then return nil end
        local _xIXX = (_oXIX.Position - nestPos) * Vector3._oooX(1, 0, 1)
        local _xOxO = _xIXX:Dot(_lIOo.Unit)
        if _xOxO < -_oolx.BEHIND_OK then return nil end
        _xOOo._oxXl = _xOOo._oxXl + 1
        return ("%s guard is %s %d studs up the route"):format(
            tostring(_oIOO), _XOOo:lower(), math.floor(math._IOoX(_xOxO, 0)))
    end
    function _xolx.blockedAreas()
        local _lxoX = {}
        local _ooxO
        pcall(function() _ooxO = workspace.__OBJECTS.Areas.GuardAreas:GetChildren() end)
        for _OXlx, _oXlx in ipairs(_ooxO or {}) do
            local _oxlx = _oXlx:FindFirstChild("Guard")
            local _IOOO = _oXlx:FindFirstChild("Bounds")
            local _XOOo = _oxlx and tostring(_oxlx:GetAttribute("GuardState") or "")
            if _oxlx and _IOOO and _IOOO:IsA("BasePart") and not _OOXl[_XOOo] then
                local _oxXX = _xolx.blocking(_oXlx.Name, _IOOO.Position)
                if _oxXX then _lxoX[_oXlx.Name] = _oxXX end
            end
        end
        return _lxoX
    end
    return _xolx
end)
_XIxX.module("features.treadmill", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _XIXo = _XIxX.require("core.data")
    local _lXxX  = _XIxX.require("core.character")
    local _OOOX = _XIxX.require("core.device")
    local _OooX = _XIxX.require("core.net")
    local _xIlx  = _XIxX.require("core.state")
    local _oloX = _XIxX.require("boot.log").for_module("treadmill")
    local _xolx = {}
    local _oolx = {
        PAD       = 6,     -- V3.1 K.TREADMILL_PAD - studs of slack on X/Z
        Y_SLACK   = 12,
        POLL      = 1.5,   -- V3.1 K.TREADMILL_POLL
        AFTER_OFF = 2.0,   -- do not re-ask while the server is acting on it
        PART_TTL  = 30,    -- how long a resolved part reference stays good
    }
    _xolx._oolx = _oolx
    local _XOx = _XIXo.plotState()
    local _xlIO = _OooX.call
    _xolx._xlIO = _xlIO
    local _OIll, _IxoO = nil, 0
    local function treadmillPart()
        local _XooX = _loIx.clock()
        if _OIll and _OIll.Parent then
            return _OIll
        end
        if not _OIll and _IxoO > 0 and (_XooX - _IxoO) < _oolx.PART_TTL then
            return nil
        end
        local _OoIo = nil
        _XIxX.try("treadmill.resolvePart", function()
            local _lOIX = _XOx and _XOx.ResolvePlot and _XOx.ResolvePlot()
            if type(_lOIX) ~= "table" or not _lOIX.PlotFolder then return end
            local _xIOx = _lOIX.PlotFolder:FindFirstChild("TreadmillBottom", true)
            if _xIOx and _xIOx:IsA("BasePart") then _OoIo = _xIOx end
        end)
        _OIll, _IxoO = _OoIo, _XooX
        return _OoIo
    end
    function _xolx.onBelt()
        local _XIIX = treadmillPart()
        local _XxOX = _lXxX._oXIX()
        if not _XIIX or not _XxOX then return false end
        local _xIXX = _XIIX.CFrame:PointToObjectSpace(_XxOX.Position)
        local _XXXo = _XIIX.Size * 0.5
        return math.abs(_xIXX.X) <= _XXXo.X + _oolx.PAD
           and math.abs(_xIXX.Z) <= _XXXo.Z + _oolx.PAD
           and math.abs(_xIXX.Y) <= _oolx.Y_SLACK
    end
    local _olxl = true     -- V3.1 default: BX.autoDoff = true
    local _lIlx = nil
    local _xOOo = { checks = 0, caught = 0, doffed = 0, refused = 0, yielded = 0, notWorn = 0 }
    function _xolx.worn()
        local _XxOX = _lXxX._oXIX()
        if _XxOX and _XxOX.Anchored then return true end
        local _xxoo = _XxOX and _XxOX.Parent
        local _XIIx = _xxoo and _xxoo:FindFirstChild("Headphones")
        return _XIIx ~= nil and _XIIx:IsA("Accessory")
    end
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    local function _oIlX()
        if not _olxl then return end
        if _xIlx.stayOnTreadmill then
            _xOOo.yielded = _xOOo.yielded + 1
            return
        end
        _xOOo.checks = _xOOo.checks + 1
        if not _xolx.onBelt() then return end
        if not _xolx.worn() then
            _xOOo.notWorn = _xOOo.notWorn + 1
            return
        end
        _xOOo.caught = _xOOo.caught + 1
        local _xOIx, _IooX = _xlIO("RF/Treadmill/AskDoff")
        if _xOIx == true then
            _xOOo.doffed = _xOOo.doffed + 1
            _oloX._XIxo("standing on the belt - AskDoff accepted")
        else
            _xOOo.refused = _xOOo.refused + 1
            _oloX.warn("standing on the belt - AskDoff refused: %s %s",
                tostring(_xOIx), tostring(_IooX or ""))
        end
        task.wait(_OOOX._oIOo(_oolx.AFTER_OFF))
    end
    function _xolx.arm()
        if _lIlx then return true end
        _lIlx = _XIxX.scope("features.treadmill")
        _lIlx:loop("watch", _OOOX._oIOo(_oolx.POLL), _oIlX)
        _lXxX.onSpawn(_lIlx, "treadmill.respawn", function()
            _OIll, _IxoO = nil, 0
        end)
        _oloX._XIxo("armed (poll %.1fs, %s)", _OOOX._oIOo(_oolx.POLL),
            _olxl and "enabled" or "disabled")
        return true
    end
    function _xolx.disarm()
        if not _lIlx then return end
        _lIlx:destroy()
        _lIlx = nil
        _OIll, _IxoO = nil, 0
        _oloX._XIxo("disarmed (%d checks, %d caught, %d doffed)",
            _xOOo.checks, _xOOo.caught, _xOOo.doffed)
    end
    function _xolx.setEnabled(_IoIx)
        _olxl = _IoIx and true or false
        _oloX._XIxo("anti treadmill %s", _olxl and "ON" or "OFF")
        if _olxl then _xolx.arm() else _xolx.disarm() end
    end
    return _xolx
end)
_XIxX.module("features.farm.filter", function(_XIxX)
    local _XIXo = _XIxX.require("core.data")
    local _OOXo = _XIxX.require("features.eggs")
    local _llX = _XIxX.require("features.guardwatch")
    local _oloX  = _XIxX.require("boot.log").for_module("farm.filter")
    local _xolx = {}
    local function AreasDir() return _XIXo.areasDir() end
    local function _Olx() return _XIXo.assetsDir() end
    local _ooxO    = {}          -- set of areaId -> true; empty = any
    local _oXol = {}          -- set of rarityId -> true; empty = any
    local _olXl = "Income"    -- "Income" | "Weight"
    local function _xIIo(_xlXX)
        local _oIOx = 0
        for _OXlx in pairs(_xlXX) do _oIOx = _oIOx + 1 end
        return _oIOx
    end
    local function toSet(_OOxo)
        local _xlXX = {}
        if type(_OOxo) == "table" then
            for _OXlx, _XlOx in pairs(_OOxo) do
                if _XlOx ~= nil and _XlOx ~= "" then _xlXX[tostring(_XlOx)] = true end
            end
        elseif type(_OOxo) == "string" and _OOxo ~= "" then
            _xlXX[_OOxo] = true
        end
        return _xlXX
    end
    function _xolx.areaOptions()
        local _lxoX = {}
        for _OlIx, entry in pairs(AreasDir() or {}) do
            _lxoX[#_lxoX + 1] = {
                _OlIx = tostring(_OlIx),
                _xxIo = tostring((type(entry) == "table" and entry.DisplayName) or _OlIx),
            }
        end
        table._lIlX(_lxoX, function(_oXlx, _XXlx) return _oXlx._xxIo < _XXlx._xxIo end)
        return _lxoX
    end
    function _xolx.rarityOptions()
        local _oxIX, _XXIX = {}, {}
        for _OXlx, entry in pairs(_Olx() or {}) do
            local _IlOx = type(entry) == "table" and entry.Rarity or nil
            if type(_IlOx) == "table" then
                local _OlIx = tostring(_IlOx._id or _IlOx.DisplayName or "")
                if _OlIx ~= "" and not _oxIX[_OlIx] then
                    _oxIX[_OlIx] = true
                    _XXIX[#_XXIX + 1] = {
                        _OlIx = _OlIx,
                        _xxIo = tostring(_IlOx.DisplayName or _OlIx),
                        num = tonumber(_IlOx.RarityNumber) or 0,
                    }
                end
            end
        end
        table._lIlX(_XXIX, function(_oXlx, _XXlx)
            if _oXlx.num ~= _XXlx.num then return _oXlx.num < _XXlx.num end
            return _oXlx._xxIo < _XXlx._xxIo
        end)
        return _XXIX
    end
    function _xolx.targetByOptions() return { "Income", "Weight" } end
    function _xolx.setAreas(_OOxo)
        _ooxO = toSet(_OOxo)
        _oloX._XIxo("areas: %s", _xIIo(_ooxO) == 0 and "any" or tostring(_xIIo(_ooxO)))
    end
    function _xolx.setRarities(_OOxo)
        _oXol = toSet(_OOxo)
        _oloX._XIxo("rarities: %s", _xIIo(_oXol) == 0 and "any" or tostring(_xIIo(_oXol)))
    end
    function _xolx.setTargetBy(_XlOx)
        _olXl = (_XlOx == "Weight") and "Weight" or "Income"
        _oloX._XIxo("target by: %s", _olXl)
    end
    function _xolx.selection()
        return { _ooxO = _ooxO, _oXol = _oXol, _olXl = _olXl }
    end
    function _xolx.describe()
        return ("%s areas, %s rarities, by %s"):format(
            _xIIo(_ooxO) == 0 and "all" or tostring(_xIIo(_ooxO)),
            _xIIo(_oXol) == 0 and "any" or tostring(_xIIo(_oXol)),
            _olXl)
    end
    local function rarityOk(_lxlx)
        if _xIIo(_oXol) == 0 then return true end
        local _OlIx = tostring(_lxlx.rarityId or _lxlx._lIXO or "")
        local _xxIo = tostring(_lxlx._lIXO or "")
        return _oXol[_OlIx] == true or _oXol[_xxIo] == true
    end
    local function wanted(_lxlx)
        if _xIIo(_ooxO) > 0 and not _ooxO[tostring(_lxlx._oIOO)] then return false end
        return rarityOk(_lxlx)
    end
    local _xlxo = { _OllX = "waiting for the first pass", _oIOx = 0, _lOIo = 0, _xoOl = nil }
    function _xolx._IXXO() return _xlxo end
    local function degradedFor(_OOxo)
        local _IXXl, _IXx = false, false
        for _OXlx, _lxlx in ipairs(_OOxo) do
            if _lxlx._oIOO ~= nil then _IXXl = true end
            if _lxlx._lIXO and _lxlx._lIXO ~= "?" then _IXx = true end
            if _IXXl and _IXx then return nil end
        end
        if _xIIo(_ooxO) > 0 and not _IXXl then
            return "eggs carry no area on this executor - clear the Areas filter"
        end
        if _xIIo(_oXol) > 0 and not _IXx then
            return "eggs carry no rarity on this executor - clear the Rarities filter"
        end
        return nil
    end
    local _xol = nil
    local _lo = 3
    local _Oll = 0
    local _XOl = 25
    function _xolx._OlIX()
        local _OOxo = _OOXo._OOxo()          -- cached; no rescan, no force
        local _lOIo = _OOxo and #_OOxo or 0
        if _lOIo == 0 then
            _xlxo = { _OllX = "no takeable eggs on the field", _oIOx = 0, _lOIo = 0 }
            return nil, "field=0 (no takeable eggs listed)"
        end
        local _xox, _OOO = 0, 0
        local _oXoo, _IxXl
        local _IoX = _loIx.clock() < _Oll
        local _oxXl = _IoX and {} or _llX.blockedAreas()
        local _xxX = {}
        for _OXlx, _lxlx in ipairs(_OOxo) do
            local _XIOO = (_xIIo(_ooxO) == 0) or _ooxO[tostring(_lxlx._oIOO)] == true
            if _XIOO then
                _xox = _xox + 1
                if rarityOk(_lxlx) and _oxXl[tostring(_lxlx._oIOO)] then
                    _xxX[tostring(_lxlx._oIOO)] = true
                elseif rarityOk(_lxlx) then
                    _OOO = _OOO + 1
                    local _xIoX = (_olXl == "Weight") and (tonumber(_lxlx._XlIx) or 0)
                                                       or (tonumber(_lxlx._XxOo) or 0)
                    if not _oXoo or _xIoX > _IxXl then _oXoo, _IxXl = _lxlx, _xIoX end
                end
            end
        end
        if _oXoo then
            _xol = nil
            _xlxo = { _OllX = ("%d of %d eggs match  \u{B7}  next: %s"):format(_OOO, _lOIo, tostring(_oXoo._oXxo)),
                     _oIOx = _OOO, _lOIo = _lOIo }
            return _oXoo, nil, _IoX
        end
        local _XXll = {}
        for _oIOO in pairs(_xxX) do _XXll[#_XXll + 1] = _oIOO end
        if #_XXll > 0 then
            local _XooX = _loIx.clock()
            _xol = _xol or _XooX
            if (_XooX - _xol) >= _lo then
                local _IXxO, _olxo
                for _OXlx, _lxlx in ipairs(_OOxo) do
                    local _XIOO = (_xIIo(_ooxO) == 0) or _ooxO[tostring(_lxlx._oIOO)] == true
                    if _XIOO and rarityOk(_lxlx) then
                        local _xIoX = (_olXl == "Weight") and (tonumber(_lxlx._XlIx) or 0) or (tonumber(_lxlx._XxOo) or 0)
                        if not _IXxO or _xIoX > _olxo then _IXxO, _olxo = _lxlx, _xIoX end
                    end
                end
                if _IXxO then
                    _oloX._XIxo("guard still out after %.0fs - going anyway for %s", _XooX - _xol, tostring(_IXxO._oXxo))
                    _xol = nil
                    _Oll = _XooX + _XOl
                    _xlxo = { _OllX = ("guard still out - going anyway  \u{B7}  next: %s"):format(tostring(_IXxO._oXxo)),
                             _oIOx = 1, _lOIo = _lOIo }
                    return _IXxO, nil, true
                end
            end
            table._lIlX(_XXll)
            local _Xllo = table.concat(_XXll, ", ")
            _xlxo = { _OllX = ("waiting for guards to go home: %s"):format(_Xllo), _oIOx = 0, _lOIo = _lOIo }
            return nil, "guards out: " .. _Xllo
        end
        local _xoOl = degradedFor(_OOxo)
        local _oxXX = ("all eggs discovered=%d area-matched=%d rarity-matched=%d target candidates=%d final eligible=0 (%s)")
            :format(_lOIo, _xox, _OOO, _OOO, _xolx.describe())
        if _xoOl then _oxXX = _oxXX .. " - " .. _xoOl end
        _xlxo = {
            _OllX = _xoOl or ("0 of %d eggs match your filters  \u{B7}  waiting"):format(_lOIo),
            _oIOx = 0, _lOIo = _lOIo, _xoOl = _xoOl,
        }
        return nil, _oxXX
    end
    function _xolx.matchCount()
        local _OOxo = _OOXo._OOxo()
        local _oIOx = 0
        for _OXlx, _lxlx in ipairs(_OOxo or {}) do
            if wanted(_lxlx) then _oIOx = _oIOx + 1 end
        end
        return _oIOx
    end
    return _xolx
end)
_XIxX.module("features.farm.treadmill_on", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _XIXo = _XIxX.require("core.data")
    local _lXxX  = _XIxX.require("core.character")
    local _OOOX = _XIxX.require("core.device")
    local _OooX = _XIxX.require("core.net")
    local _xIlx  = _XIxX.require("core.state")
    local _oloX = _XIxX.require("boot.log").for_module("farm.treadmill")
    local _xolx = {}
    local _oolx = {
        POLL     = 1.0,    -- how often to check we are still on the spot
        DRIFT    = 6,      -- studs away from the spot before nudging back
        STEP_OFF = 14,     -- how far clear to stand when releasing
    }
    _xolx._oolx = _oolx
    local _XOx = _XIXo.plotState()
    local _lIlx = nil
    local _olxl = false
    local _xOOo = { nudges = 0, paused = 0, doffed = 0, noSpot = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    function _xolx._OIlX()
        local _xxIX
        _XIxX.try("farm.treadmill.slot", function()
            _xxIX = _XOx and _XOx.ResolveLocalSlot and _XOx.ResolveLocalSlot()
        end)
        if not _xxIX then return nil end
        local _IIXX
        _XIxX.try("farm.treadmill.spot", function()
            local _IIoO = workspace:FindFirstChild("__ClientTreadmillRenders")
            local _OlXO = _IIoO and _IIoO:FindFirstChild("TreadmillRender_" .. tostring(_xxIX))
            local _oXIX = _OlXO and _OlXO:FindFirstChild("Root")
            if _oXIX and _oXIX:IsA("BasePart") then
                _IIXX = _oXIX.Position
                return
            end
            local _oXlo = workspace:FindFirstChild("Plots")
            local _lOIX = _oXlo and _oXlo:FindFirstChild(tostring(_xxIX))
            local _xlOO = _lOIX and _lOIX:FindFirstChild("TreadmillBottom")
            if _xlOO and _xlOO:IsA("BasePart") then
                _IIXX = _xlOO.Position + Vector3._oooX(0, 4, 0)
            end
        end)
        return _IIXX
    end
    local function place(_IIXX)
        local _XxOX = _lXxX._oXIX()
        if not _XxOX or not _IIXX then return false end
        local _xOIx = _XIxX.try("farm.treadmill.place", function()
            _XxOX.CFrame = CFrame._oooX(_IIXX)
        end)
        return _xOIx and true or false
    end
    local function _oIlX()
        if not _olxl then return end
        if _xIlx.autoStealOn then
            _xOOo.paused = _xOOo.paused + 1
            return
        end
        local _IIXX = _xolx._OIlX()
        if not _IIXX then
            _xOOo.noSpot = _xOOo.noSpot + 1
            return
        end
        local _XxOX = _lXxX._oXIX()
        if not _XxOX then return end
        if (_XxOX.Position - _IIXX).Magnitude > _oolx.DRIFT then
            if place(_IIXX) then
                _xOOo.nudges = _xOOo.nudges + 1
                _oloX.trace("nudged back onto the belt")
            end
        end
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        if _IoIx then
            if _xIlx.autoStealOn then
                _oloX.warn("refused - Auto Steal is running")
                return false, "Turn Auto Steal off first"
            end
            local _IIXX = _xolx._OIlX()
            if not _IIXX then
                _oloX.warn("refused - could not resolve your treadmill")
                return false, "Could not find your treadmill"
            end
            _olxl = true
            _xIlx.stayOnTreadmill = true          -- Anti Treadmill stands down
            _XIxX.require("core.motion").claim("hold")   -- Fly and Speed stand down
            place(_IIXX)
            _lIlx = _XIxX.scope("features.farm.treadmill_on")
            _lIlx:loop("hold", _OOOX._oIOo(_oolx.POLL), _oIlX)
            _lXxX.onSpawn(_lIlx, "farm.treadmill.respawn", function()
                if _olxl and not _xIlx.autoStealOn then place(_xolx._OIlX()) end
            end)
            _oloX._XIxo("holding on the belt (poll %.1fs)", _OOOX._oIOo(_oolx.POLL))
            return true
        end
        _olxl = false
        _xIlx.stayOnTreadmill = false
        _XIxX.require("core.motion").release("hold")
        if _lIlx then _lIlx:destroy() _lIlx = nil end
        local _xOIx, _IooX = _OooX.call("RF/Treadmill/AskDoff")
        if _xOIx == true then
            _xOOo.doffed = _xOOo.doffed + 1
        else
            _oloX.warn("AskDoff refused: %s %s", tostring(_xOIx), tostring(_IooX or ""))
        end
        local _IIXX = _xolx._OIlX()
        if _IIXX then place(_IIXX + Vector3._oooX(0, 3, _oolx.STEP_OFF)) end
        _oloX._XIxo("released (%d nudges, %d paused for a run)", _xOOo.nudges, _xOOo.paused)
        return true
    end
    _XIxX.onTeardown("farm.treadmill_on", function() if _olxl then _xolx.setEnabled(false) end end)
    return _xolx
end)
_XIxX.module("features.farm.pets", function(_XIxX)
    local _OooX = _XIxX.require("core.net")
    local _oloX = _XIxX.require("boot.log").for_module("farm.pets")
    local _xolx = {}
    local _xOOo = { asked = 0, _XXOl = 0, refused = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.equipBest()
        _xOOo.asked = _xOOo.asked + 1
        local _xOIx, _IooX = _OooX.call("RF/Haul/WearBest")
        if _xOIx == true then
            _xOOo._XXOl = _xOOo._XXOl + 1
            _oloX._XIxo("equipped best pets")
            return true, "Equipped your best pets"
        end
        _xOOo.refused = _xOOo.refused + 1
        _oloX.warn("WearBest refused: %s %s", tostring(_xOIx), tostring(_IooX or ""))
        return false, "Refused: " .. tostring(_IooX or _xOIx)
    end
    return _xolx
end)
_XIxX.module("features.farm.plotcare", function(_XIxX)
    local _OoXX   = _XIxX.require("core.services")
    local _OOOX   = _XIxX.require("core.device")
    local _xIlx    = _XIxX.require("core.state")
    local _XIXo  = _XIxX.require("core.data")
    local _OOXo  = _XIxX.require("features.eggs")
    local _oloX   = _XIxX.require("boot.log").for_module("farm.plotcare")
    local _xolx = {}
    local _oolx = {
        TICK          = 5,     -- backstop check, seconds
        HATCH_GAP     = 1.5,   -- BeginHatch -> FinishHatch (the game plays an animation here)
        FINISH_TRIES  = 4,     -- FinishHatch retries, HATCH_GAP apart
        PLACE_GAP     = 0.6,   -- between placements
        WEAR_WAIT     = 1.5,   -- for the worn egg tool to appear
        SPACING       = 7,     -- grid pitch on the PetArea, studs
        MARGIN        = 4,     -- keep off the PetArea edge
        CLEARANCE     = 5.5,   -- min distance from an egg already placed
        SPOT_TRIES    = 3,     -- spots tried per egg before giving up on it
        REFUSED_WAIT  = 30,    -- after the server refuses to place anything
        NEAR          = 35,
        WALK_TIMEOUT  = 8,
        RANGE_WAIT    = 4,     -- retry soon after an out-of-range refusal
    }
    _xolx._oolx = _oolx
    local _lXIO, _OXxl = false, false
    local _OXIO, _oXxl = nil, nil
    local _lxx, _Ixx = false, false
    local _Il = 0
    local _lXIl, _xoIl = "off", "off"
    local _xOOo = { _XxoO = 0, placeRefused = 0, hatched = 0, hatchRefused = 0, finishRetries = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isPlacing() return _lXIO end
    function _xolx.isHatching() return _OXxl end
    local function _OOIx()
        local _IOIx = _OoXX.Players.LocalPlayer
        return _IOIx and _IOIx.UserId
    end
    local function ownedEggs()
        local _xIxX = _XIXo.eggState()
        local _XoIX = {}
        _XIxX.try("plotcare.readOwner", function()
            _XoIX = (_xIxX and _xIxX.ReadOwnerEggs and _xIxX.ReadOwnerEggs(_OOIx())) or {}
        end)
        return _XoIX, _xIxX
    end
    local function inArena()
        local _IOIx = _OoXX.Players.LocalPlayer
        return _IOIx ~= nil and _IOIx:GetAttribute("InBossArena") == true
    end
    local function hatchOne(_xIxX, _OXXX)
        local _xOIx, _IooX, _olXO = false, nil, nil
        _XIxX.try("plotcare.beginHatch", function() _xOIx, _IooX, _olXO = _xIxX.BeginHatch(_OXXX) end)
        if not _xOIx then
            _xOOo.hatchRefused = _xOOo.hatchRefused + 1
            _xoIl = "refused: " .. tostring(_IooX or "no reason given")
            _oloX.warn("BeginHatch refused for %s: %s", _OXXX, tostring(_IooX))
            return false
        end
        for _xXXl = 1, _oolx.FINISH_TRIES do
            task.wait(_oolx.HATCH_GAP)
            if not _OXxl then return false end
            local _xoOX, _loXo, _xoxl = false, nil, nil
            _XIxX.try("plotcare.finishHatch", function() _xoOX, _loXo, _xoxl = _xIxX.FinishHatch(_OXXX) end)
            if _xoOX then
                _xOOo.hatched = _xOOo.hatched + 1
                _xoIl = ("hatched %d this session"):format(_xOOo.hatched)
                _oloX._XIxo("hatched %s -> %s%s", _OXXX, tostring(_xoxl),
                    _olXO and (" (" .. tostring(_olXO) .. ")") or "")
                return true
            end
            _xOOo.finishRetries = _xOOo.finishRetries + 1
            _oloX.warn("FinishHatch %d/%d for %s: %s", _xXXl, _oolx.FINISH_TRIES, _OXXX, tostring(_loXo))
            _xoIl = "finishing: " .. tostring(_loXo or "waiting")
        end
        return false
    end
    local function hatchPass()
        if not _OXxl or _Ixx then return end
        if _xIlx.autoStealOn then _xoIl = "waiting for Auto Steal" return end
        _Ixx = true
        _XIxX.try("plotcare.hatchPass", function()
            local _XoIX, _xIxX = ownedEggs()
            if not (_xIxX and _xIxX.IsReadyToHatch and _xIxX.BeginHatch and _xIxX.FinishHatch) then
                _xoIl = "hatch API unavailable"
                return
            end
            local _XxoO, _Xxlo = 0, {}
            for _OXXX, _XIXX in pairs(_XoIX) do
                if _XIXX.Placement ~= nil then
                    _XxoO = _XxoO + 1
                    local _IIIO = false
                    _XIxX.try("plotcare.ready", function() _IIIO = _xIxX.IsReadyToHatch(_OXXX) == true end)
                    if _IIIO then _Xxlo[#_Xxlo + 1] = _OXXX end
                end
            end
            if #_Xxlo == 0 then
                _xoIl = _XxoO == 0 and "nothing placed" or ("%d growing"):format(_XxoO)
                return
            end
            for _OXlx, _OXXX in ipairs(_Xxlo) do
                if not _OXxl or _xIlx.autoStealOn then break end
                hatchOne(_xIxX, _OXXX)
            end
        end)
        _Ixx = false
    end
    local function freeSpots(_lOIX)
        local _looo, _OoOO = _lOIX.PetArea, _lOIX.CenterPoint
        if not (_looo and _OoOO and _looo:IsA("BasePart")) then return {} end
        local _xoOo = {}
        local _IIoO = workspace:FindFirstChild("PlacedEggRenders")
        local _xxoO = tostring(_OOIx()) .. "_"
        if _IIoO then
            for _OXlx, _OIOx in ipairs(_IIoO:GetChildren()) do
                if _OIOx:IsA("Model") and _OIOx.Name:_loXX(1, #_xxoO) == _xxoO then
                    _XIxX.try("plotcare.pivot", function() _xoOo[#_xoOo + 1] = _OIOx:GetPivot().Position end)
                end
            end
        end
        local _XXXo = _looo.Size * 0.5
        local _xlOo = {}
        for _IOOx = -_XXXo.X + _oolx.MARGIN, _XXXo.X - _oolx.MARGIN, _oolx.SPACING do
            for _OOOx = -_XXXo.Z + _oolx.MARGIN, _XXXo.Z - _oolx.MARGIN, _oolx.SPACING do
                local _XIoo = (_looo.CFrame * CFrame._oooX(_IOOx, _XXXo.Y, _OOOx)).Position
                local _lIIo = true
                for _OXlx, _xIOx in ipairs(_xoOo) do
                    local _IoXo = Vector3._oooX(_xIOx.X - _XIoo.X, 0, _xIOx.Z - _XIoo.Z)
                    if _IoXo.Magnitude < _oolx.CLEARANCE then _lIIo = false break end
                end
                if _lIIo then
                    _xlOo[#_xlOo + 1] = _OoOO.CFrame:ToObjectSpace(CFrame._oooX(_XIoo))
                end
            end
        end
        return _xlOo
    end
    local function wornEggToolUid(_xOlO)
        local _IOIx = _OoXX.Players.LocalPlayer
        local _XoOl = _loIx.clock() + (_xOlO or 0)
        repeat
            local _xxoo = _IOIx and _IOIx.Character
            if _xxoo then
                for _OXlx, _Ixlx in ipairs(_xxoo:GetChildren()) do
                    if _Ixlx:IsA("Tool") and _Ixlx:GetAttribute("ItemType") == "AssetEgg" then
                        local _OXXX = _Ixlx:GetAttribute("UID")
                        if type(_OXXX) == "string" and _OXXX ~= "" then return _OXXX end
                    end
                end
            end
            if _loIx.clock() >= _XoOl then break end
            task.wait(0.05)
        until false
        return nil
    end
    local function unplacedByValue(_XoIX)
        local _OOxo = {}
        for _OXXX, _XIXX in pairs(_XoIX) do
            if _XIXX.Placement == nil then
                local _XlOx = 0
                _XIxX.try("plotcare.value", function()
                    _XlOx = _OOXo._XxOo({ Uid = _OXXX, AssetCategory = _XIXX.AssetCategory,
                                     AssetScale = _XIXX.AssetScale, Mutations = _XIXX.Mutations }) or 0
                end)
                _OOxo[#_OOxo + 1] = { _OXXX = _OXXX, _XxOo = tonumber(_XlOx) or 0, _oXxo = tostring(_XIXX.AssetCategory) }
            end
        end
        table._lIlX(_OOxo, function(_oXlx, _XXlx) return _oXlx._XxOo > _XXlx._XxOo end)
        return _OOxo
    end
    local function placeOne(_xIxX, _lOIX, _xOOX)
        local _xxXX, _IXlX = false, nil
        _XIxX.try("plotcare.wear", function() _xxXX, _IXlX = _xIxX.WearEggTool(_xOOX._OXXX) end)
        if not _xxXX then
            return false, "could not hold the egg: " .. tostring(_IXlX or "refused")
        end
        local _IolO = wornEggToolUid(_oolx.WEAR_WAIT) or _xOOX._OXXX
        local _xlOo = freeSpots(_lOIX)
        if #_xlOo == 0 then
            _XIxX.try("plotcare.doff", function() _xIxX.DoffEggTool(_IolO) end)
            return false, "no free space on the plot"
        end
        local _OIIO
        for _xxlx = 1, math.min(_oolx.SPOT_TRIES, #_xlOo) do
            local _OIlX = _xlOo[((_xOOo._XxoO + _xxlx - 1) % #_xlOo) + 1]
            local _xOIx, _IooX = false, nil
            _XIxX.try("plotcare.plant", function() _xOIx, _IooX = _xIxX.PlantEgg(_IolO, _OIlX) end)
            if _xOIx then
                _xOOo._XxoO = _xOOo._XxoO + 1
                _oloX._XIxo("placed %s (%s)", _xOOX._oXxo, _IolO)
                return true
            end
            _OIIO = _IooX
            _oloX.warn("PlantEgg refused (%s): %s", _xOOX._oXxo, tostring(_IooX))
        end
        _XIxX.try("plotcare.doff", function() _xIxX.DoffEggTool(_IolO) end)
        return false, tostring(_OIIO or "refused")
    end
    local _xxxl = false
    local _xOX = _oolx.NEAR
    local function isRangeRefusal(_IooX)
        return type(_IooX) == "string" and _IooX:lower():find("closer", 1, true) ~= nil
    end
    local function walkToPlot(_lOIX)
        local _IOIx = _OoXX.Players.LocalPlayer
        local _xxoo = _IOIx and _IOIx.Character
        local _IIoX = _xxoo and _xxoo:FindFirstChildOfClass("Humanoid")
        local _oXIX = _xxoo and _xxoo:FindFirstChild("HumanoidRootPart")
        local _OIOO = _lOIX.CenterPoint or _lOIX.PetArea
        if not (_IIoX and _oXIX and _OIOO and _OIOO:IsA("BasePart")) then
            return false, "no character or plot to walk to"
        end
        local _xXXO = _OIOO.Position
        local function flatDist()
            local _Ixlx = _oXIX.Position - _xXXO
            return Vector3._oooX(_Ixlx.X, 0, _Ixlx.Z).Magnitude
        end
        if flatDist() <= _xOX then return true end
        if _IIoX.Health <= 0 then return false, "character is dead" end
        _lXIl = "walking to your plot"
        _oloX._XIxo("walking to the plot to place (%.0f studs away)", flatDist())
        local _XoOl = _loIx.clock() + _oolx.WALK_TIMEOUT
        local _IXIl = 0
        while _loIx.clock() < _XoOl do
            if not _lXIO or (_xIlx.autoStealOn and not _xxxl) or _xIlx.stayOnTreadmill or inArena() then
                return false, "interrupted"
            end
            if _loIx.clock() - _IXIl >= 1 then
                _IXIl = _loIx.clock()
                _IIoX:MoveTo(_xXXO)
            end
            if flatDist() <= _xOX then
                _IIoX:MoveTo(_oXIX.Position)   -- stop there, not at the exact centre
                return true
            end
            task.wait(0.1)
        end
        return false, "could not walk to your plot"
    end
    local function placePass()
        if not _lXIO or _lxx then return end
        if _loIx.clock() < _Il and not _xxxl then return end
        if _xIlx.autoStealOn and not _xxxl then _lXIl = "waiting for Auto Steal" return end
        if _xIlx.stayOnTreadmill then _lXIl = "waiting for the treadmill hold" return end
        if inArena() then _lXIl = "waiting - in the boss arena" return end
        _lxx = true
        _XIxX.try("plotcare.placePass", function()
            local _XoIX, _xIxX = ownedEggs()
            local _llxX = _XIXo.plotState()
            if not (_xIxX and _xIxX.WearEggTool and _xIxX.PlantEgg and _xIxX.DoffEggTool and _llxX) then
                _lXIl = "place API unavailable"
                return
            end
            local _lOIX
            _XIxX.try("plotcare.plot", function() _lOIX = _llxX.ResolvePlot() end)
            if type(_lOIX) ~= "table" then _lXIl = "could not find your plot" return end
            local _xllX = unplacedByValue(_XoIX)
            if #_xllX == 0 then _lXIl = "no eggs to place" return end
            local _XXxo, _OIxO = walkToPlot(_lOIX)
            if not _XXxo then
                _lXIl = "waiting: " .. tostring(_OIxO)
                _Il = _loIx.clock() + _oolx.RANGE_WAIT
                return
            end
            for _OXlx, _xOOX in ipairs(_xllX) do
                if not _lXIO or (_xIlx.autoStealOn and not _xxxl) or _xIlx.stayOnTreadmill then break end
                local _xOIx, _XIlX = placeOne(_xIxX, _lOIX, _xOOX)
                if not _xOIx then
                    _xOOo.placeRefused = _xOOo.placeRefused + 1
                    if isRangeRefusal(_XIlX) then
                        _lXIl = "getting closer to your plot"
                        _Il = _loIx.clock() + _oolx.RANGE_WAIT
                        if _xOX > 8 then
                            _xOX = 8
                            _oloX._XIxo("still out of range - walking to the plot centre from now on")
                        end
                    else
                        _lXIl = "stopped: " .. tostring(_XIlX)
                        _Il = _loIx.clock() + _oolx.REFUSED_WAIT
                    end
                    break
                end
                _lXIl = ("placed %d this session"):format(_xOOo._XxoO)
                task.wait(_oolx.PLACE_GAP)
            end
        end)
        _lxx = false
    end
    local function arm(_oXxo, _xIIX)
        local _lIlx = _XIxX.scope("features.farm.plotcare." .. _oXxo)
        _lIlx:loop(_oXxo, _OOOX._oIOo(_oolx.TICK), _xIIX)
        _XIxX.try("plotcare.watch." .. _oXxo, function()
            local _xIxX = _XIXo.eggState()
            if _xIxX and _xIxX.OwnerRefreshed then
                _lIlx:connect(_xIxX.OwnerRefreshed, function(_XxXO)
                    if _XxXO ~= _OOIx() then return end
                    task.spawn(function() _XIxX.try("plotcare.onOwner." .. _oXxo, _xIIX) end)
                end)
            end
        end)
        task.spawn(function() _XIxX.try("plotcare.first." .. _oXxo, _xIIX) end)
        return _lIlx
    end
    function _xolx.placeNow()
        if not _lXIO then return false end
        local _Ollx = _loIx.clock()
        while _lxx and _loIx.clock() - _Ollx < 10 do task.wait(0.1) end
        for _xXXl = 1, 4 do
            local _XoIX = ownedEggs()
            local _lIOX = false
            for _OXlx, _XIXX in pairs(_XoIX) do
                if _XIXX.Placement == nil then _lIOX = true break end
            end
            if _lIOX then break end
            if _xXXl == 4 then return true end
            task.wait(0.5)
        end
        _xxxl = true
        _Il = 0
        _XIxX.try("plotcare.placeNow", placePass)
        _xxxl = false
        return true
    end
    function _xolx.setPlace(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _lXIO then return true end
        _lXIO = _IoIx
        if _OXIO then _OXIO:destroy() _OXIO = nil end
        if _IoIx then
            _Il = 0
            _lXIl = "starting"
            _OXIO = arm("place", placePass)
        else
            _lXIl = "off"
        end
        _oloX._XIxo("auto place %s", _IoIx and "ON" or "OFF")
        return true
    end
    function _xolx.setHatch(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _OXxl then return true end
        _OXxl = _IoIx
        if _oXxl then _oXxl:destroy() _oXxl = nil end
        if _IoIx then
            _xoIl = "starting"
            _oXxl = arm("hatch", hatchPass)
        else
            _xoIl = "off"
        end
        _oloX._XIxo("auto hatch %s", _IoIx and "ON" or "OFF")
        return true
    end
    function _xolx.preview()
        local _XoIX, _xIxX = ownedEggs()
        local _lxoX = { _XxoO = 0, _Xxlo = 0, unplaced = 0, freeSpots = 0, nextEgg = nil }
        for _OXXX, _XIXX in pairs(_XoIX) do
            if _XIXX.Placement ~= nil then
                _lxoX._XxoO = _lxoX._XxoO + 1
                _XIxX.try("plotcare.previewReady", function()
                    if _xIxX.IsReadyToHatch(_OXXX) then _lxoX._Xxlo = _lxoX._Xxlo + 1 end
                end)
            else
                _lxoX.unplaced = _lxoX.unplaced + 1
            end
        end
        local _Oolo = unplacedByValue(_XoIX)
        _lxoX.nextEgg = _Oolo[1] and _Oolo[1]._oXxo or nil
        local _llxX = _XIXo.plotState()
        _XIxX.try("plotcare.previewPlot", function()
            local _lOIX = _llxX and _llxX.ResolvePlot()
            if type(_lOIX) == "table" then _lxoX.freeSpots = #freeSpots(_lOIX) end
        end)
        return _lxoX
    end
    function _xolx._IXXO()
        return ("Place: %s  \u{B7}  Hatch: %s"):format(_lXIl, _xoIl)
    end
    return _xolx
end)
_XIxX.module("features.esp.cards", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _OOOX = _XIxX.require("core.device")
    local _oloX = _XIxX.require("boot.log").for_module("esp.cards")
    local _xolx = {}
    local _oolx = {
        W = 190, H = 40,
        VIS_HZ = 12,          -- V3.1 K.ESP_VIS_HZ cadence for the size follow
        MAX_DIST = 2200,      -- V3.1 K.ESP_MAX_DIST
        FADE_BAND = 260,      -- V3.1 K.ESP_FADE_BAND
        BASE_ALPHA = 0.42,    -- V3.1 frame.BackgroundTransparency
        BASE_STROKE = 0.55,
        BUILD_PER_FRAME = 3,
    }
    _xolx._oolx = _oolx
    local _Oolx = {
        bgTop   = Color3.fromRGB(26, 26, 30),
        bgBot   = Color3.fromRGB(14, 14, 17),
        _IIOO  = Color3.fromRGB(206, 206, 212),
        element = Color3.fromRGB(41, 41, 48),
        _OXOo   = Color3.fromRGB(246, 242, 234),
        _loXX     = Color3.fromRGB(168, 158, 144),
    }
    _xolx._xlxO = {
        titleFont = Enum.Font.GothamBold, titleSize = 13,
        subFont = Enum.Font.GothamBold,     subSize   = 10,
    }
    _xolx._oXlX = {
        income = "57F287", neutral = "F0F0F6", mutation = "F0BE5A",
        dim = "8A8A92", _Xxlo = "57F287",
    }
    _xolx._lxlX = "  \u{B7}  "
    function _xolx._XllX(col, _OllX)
        return ('<font color="#%s">%s</font>'):format(col, _OllX)
    end
    function _xolx._IxOX(_xXlx)
        return ("%02X%02X%02X"):format(
            math.floor(_xXlx.R * 255 + 0.5), math.floor(_xXlx.G * 255 + 0.5),
            math.floor(_xXlx.B * 255 + 0.5))
    end
    local function scaleFor(_xlXo)
        return math.clamp(1.25 - (tonumber(_xlXo) or 0) / 800, 0.6, 1.25)
    end
    local _lIlx, _IIoO, _lXxl = nil, nil, 0
    local _XXlo = {}      -- handle name -> { cards }
    local _XXxO, _OoxO
    local function ensure()
        if _lIlx then return end
        _lIlx = _XIxX.scope("features.esp.cards")
        _IIoO = Instance._oooX("Folder")
        _IIoO.Name = "RyuzakiESP"
        _lIlx:own(_IIoO)
        _IIoO.Parent = workspace
        local _XxlX, _oIlX = 0, 1 / _oolx.VIS_HZ
        _lIlx:onFrame("vis", _OoXX.RunService.RenderStepped, function(_xXxX)
            local _OOOO = _OOOX._OOOO(_oolx.BUILD_PER_FRAME)
            for _OXlx, _OOIX in pairs(_XXlo) do
                if _OOOO <= 0 then break end
                for _xxlx, _Ixlx in pairs(_OOIX._OoIO) do
                    if _OOOO <= 0 then break end
                    local _xXlx = _XXxO()
                    _OOIX[_xxlx] = _xXlx
                    _OOIX._oIOx = _OOIX._oIOx + 1
                    if _xxlx > _OOIX.high then _OOIX.high = _xxlx end
                    _OoxO(_xXlx, _Ixlx)
                    _OOIX._OoIO[_xxlx] = nil
                    _OOOO = _OOOO - 1
                end
            end
            _XxlX = _XxlX + (_xXxX or 0)
            if _XxlX < _oIlX then return end
            _XxlX = 0
            local _llOX = workspace.CurrentCamera
            if not _llOX then return end
            local _OoOX = _llOX.CFrame.Position
            for _OXlx, _OOIX in pairs(_XXlo) do
                for _xxlx = 1, _OOIX._llOo do
                    local _xXlx = _OOIX[_xxlx]
                    if _xXlx and _xXlx._OIOO.Parent then
                        local _Ixlx = (_xXlx._IIXX - _OoOX).Magnitude
                        local _XxIX = _Ixlx <= _oolx.MAX_DIST
                        if _xXlx._xOxX.Enabled ~= _XxIX then _xXlx._xOxX.Enabled = _XxIX end
                        if _XxIX then
                            local _llOx = scaleFor(_Ixlx)
                            if math.abs(_xXlx.lastScale - _llOx) > 0.01 or _xXlx.lastH ~= _xXlx.baseH then
                                _xXlx.lastScale, _xXlx.lastH = _llOx, _xXlx.baseH
                                _xXlx._oIOo.Scale = _llOx
                                _xXlx._xOxX.Size = UDim2.fromOffset(_oolx.W * _llOx, _xXlx.baseH * _llOx)
                            end
                            local _xOXo = math.clamp((_oolx.MAX_DIST - _Ixlx) / _oolx.FADE_BAND, 0, 1)
                            if math.abs(_xXlx.lastFade - _xOXo) > 0.02 then
                                _xXlx.lastFade = _xOXo
                                _xXlx._ooIo.BackgroundTransparency = 1 - (1 - _oolx.BASE_ALPHA) * _xOXo
                                _xXlx._OXOo.TextTransparency = 1 - _xOXo
                                _xXlx._loXX.TextTransparency = 1 - _xOXo
                                _xXlx._OIxo.ImageTransparency = 1 - _xOXo
                                _xXlx._OXXO.Transparency = 1 - (1 - _oolx.BASE_STROKE) * _xOXo
                            end
                        end
                    end
                end
            end
        end)
    end
    function _XXxO()
        local _OIOO = Instance._oooX("Part")
        _OIOO.Name = "EggAnchor"
        _OIOO.Anchored = true
        _OIOO.CanCollide = false
        _OIOO.CanQuery = false
        _OIOO.CanTouch = false
        _OIOO.CastShadow = false
        _OIOO.Transparency = 1
        _OIOO.Size = Vector3._oooX(0.2, 0.2, 0.2)
        _OIOO.Parent = _IIoO
        local _xOxX = Instance._oooX("BillboardGui")
        _xOxX.Name = "EggCard"
        _xOxX.AlwaysOnTop = true
        _xOxX.LightInfluence = 0
        _xOxX.MaxDistance = 1e6          -- not math.huge: some clients reject inf
        _xOxX.Size = UDim2.fromOffset(_oolx.W, _oolx.H)
        _xOxX.StudsOffset = Vector3._oooX(0, 3, 0)
        _xOxX.Active = false
        _xOxX.Adornee = _OIOO
        _xOxX.Enabled = false
        _xOxX.Parent = _OIOO
        local _ooIo = Instance._oooX("Frame")
        _ooIo.Size = UDim2.fromOffset(_oolx.W, _oolx.H)
        _ooIo.BackgroundColor3 = Color3._oooX(1, 1, 1)
        _ooIo.BackgroundTransparency = _oolx.BASE_ALPHA
        _ooIo.BorderSizePixel = 0
        _ooIo.ClipsDescendants = true
        _ooIo.Parent = _xOxX
        Instance._oooX("UICorner", _ooIo).CornerRadius = UDim._oooX(0, 0)
        local _OXXo = Instance._oooX("UIGradient", _ooIo)
        _OXXo.Color = ColorSequence._oooX(_Oolx.bgTop, _Oolx.bgBot)
        _OXXo.Rotation = 90
        local _Xxol = Instance._oooX("UIScale")
        _Xxol.Scale = 1
        _Xxol.Parent = _ooIo
        local _OXXO = Instance._oooX("UIStroke", _ooIo)
        _OXXO.Color = Color3._oooX(1, 1, 1)
        _OXXO.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
        _OXXO.Thickness = 1
        _OXXO.Transparency = _oolx.BASE_STROKE
        local _oIlx = Instance._oooX("UIGradient", _OXXO)
        _oIlx.Color = ColorSequence._oooX(_Oolx._IIOO, _Oolx.element)
        _oIlx.Rotation = 90
        local _IIOO = Instance._oooX("Frame")
        _IIOO.Name = "Accent"
        _IIOO.Position = UDim2.fromOffset(3, 4)
        _IIOO.Size = UDim2._oooX(0, 2, 1, -8)
        _IIOO.BorderSizePixel = 0
        _IIOO.BackgroundColor3 = Color3.fromRGB(194, 142, 54)
        _IIOO.Parent = _ooIo
        Instance._oooX("UICorner", _IIOO).CornerRadius = UDim._oooX(0, 0)
        local _OIxo = Instance._oooX("ImageLabel")
        _OIxo.Name = "Icon"
        _OIxo.Position = UDim2.fromOffset(9, 8)
        _OIxo.Size = UDim2.fromOffset(24, 24)
        _OIxo.BackgroundTransparency = 1
        _OIxo.ScaleType = Enum.ScaleType.Fit
        _OIxo.Image = ""
        _OIxo.Parent = _ooIo
        local _OXOo = Instance._oooX("TextLabel")
        _OXOo.Name = "Title"
        _OXOo.Position = UDim2.fromOffset(38, 3)
        _OXOo.Size = UDim2._oooX(1, -44, 0, 15)
        _OXOo.BackgroundTransparency = 1
        _OXOo.Font = Enum.Font.GothamBold
        _OXOo.TextSize = 12
        _OXOo.TextColor3 = _Oolx._OXOo
        _OXOo.TextXAlignment = Enum.TextXAlignment.Left
        _OXOo.TextTruncate = Enum.TextTruncate.AtEnd
        _OXOo.Text = ""
        _OXOo.Parent = _ooIo
        local _loXX = Instance._oooX("TextLabel")
        _loXX.Name = "Sub"
        _loXX.Position = UDim2.fromOffset(38, 18)
        _loXX.Size = UDim2._oooX(1, -44, 0, 20)
        _loXX.BackgroundTransparency = 1
        _loXX.Font = Enum.Font.GothamBold
        _loXX.TextSize = 10
        _loXX.TextColor3 = _Oolx._loXX
        _loXX.TextXAlignment = Enum.TextXAlignment.Left
        _loXX.TextYAlignment = Enum.TextYAlignment.Top
        _loXX.RichText = true          -- the rarity is coloured inline, as in V3.1
        _loXX.Text = ""
        _loXX.Parent = _ooIo
        return {
            _OIOO = _OIOO, _xOxX = _xOxX, _ooIo = _ooIo, _OXXO = _OXXO,
            _IIOO = _IIOO, _OIxo = _OIxo, _OXOo = _OXOo, _loXX = _loXX,
            _oIOo = _Xxol, _IIXX = Vector3.zero, baseH = _oolx.H,
            lastScale = -1, lastFade = -1, lastH = -1,
            lastTitle = nil, lastSub = nil, lastIcon = nil, lastStyle = nil,
        }
    end
    function _OoxO(_xXlx, _Ixlx)
        if _xXlx._IIXX ~= _Ixlx._IIXX then
            _xXlx._IIXX = _Ixlx._IIXX
            _xXlx._OIOO.CFrame = CFrame._oooX(_Ixlx._IIXX)
        end
        local _Xxlx = (_Ixlx._Illo and _Ixlx._Illo > 1) and (_oolx.H + 12) or _oolx.H
        if _xXlx.baseH ~= _Xxlx then
            _xXlx.baseH = _Xxlx
            _xXlx._ooIo.Size = UDim2.fromOffset(_oolx.W, _Xxlx)
            _xXlx._loXX.Size = UDim2._oooX(1, -44, 0, _Xxlx - 20)
        end
        local _lXll = (_Ixlx._xXXO and "\u{25B8} " or "") .. tostring(_Ixlx._OXOo or "")
        if _lXll ~= _xXlx.lastTitle then
            _xXlx.lastTitle = _lXll
            _xXlx._OXOo.Text = _lXll
        end
        if _Ixlx._loXX ~= _xXlx.lastSub then
            _xXlx.lastSub = _Ixlx._loXX
            _xXlx._loXX.Text = tostring(_Ixlx._loXX or "")
        end
        if _Ixlx._OIxo ~= _xXlx.lastIcon then
            _xXlx.lastIcon = _Ixlx._OIxo
            _xXlx._OIxo.Image = tostring(_Ixlx._OIxo or "")
        end
        if _Ixlx._IIOO and _Ixlx._IIOO ~= _xXlx.lastAccent then
            _xXlx.lastAccent = _Ixlx._IIOO
            _xXlx._IIOO.BackgroundColor3 = _Ixlx._IIOO
        end
        local _xIlx = _Ixlx._OoOo
        if _xIlx ~= _xXlx.lastStyle then
            _xXlx.lastStyle = _xIlx
            _xXlx._OXOo.Font = (_xIlx and _xIlx.titleFont) or Enum.Font.GothamBold
            _xXlx._OXOo.TextSize = (_xIlx and _xIlx.titleSize) or 12
            _xXlx._loXX.Font = (_xIlx and _xIlx.subFont) or Enum.Font.Gotham
            _xXlx._loXX.TextSize = (_xIlx and _xIlx.subSize) or 10
        end
    end
    local _OxlO = {}
    _OxlO.__index = _OxlO
    function _OxlO:_XxIX(_xxlx, _Ixlx)
        local _OOIX = _XXlo[self._oXxo]
        local _xXlx = _OOIX[_xxlx]
        if not _xXlx then
            _OOIX._OoIO[_xxlx] = _Ixlx
            return
        end
        _OoxO(_xXlx, _Ixlx)
    end
    function _OxlO:_llOo(_oIOx)
        local _OOIX = _XXlo[self._oXxo]
        _OOIX._llOo = _oIOx
        for _xxlx = _oIOx + 1, _OOIX.high do
            local _xXlx = _OOIX[_xxlx]
            if _xXlx and _xXlx._xOxX.Enabled then _xXlx._xOxX.Enabled = false end
        end
        for _xxlx in pairs(_OOIX._OoIO) do
            if _xxlx > _oIOx then _OOIX._OoIO[_xxlx] = nil end
        end
    end
    function _OxlO:_xIIo()
        local _OOIX = _XXlo[self._oXxo]
        return _OOIX._oIOx, _OOIX._llOo
    end
    function _OxlO:close()
        local _OOIX = _XXlo[self._oXxo]
        for _xxlx = 1, _OOIX.high do
            local _xXlx = _OOIX[_xxlx]
            if _xXlx then pcall(function() _xXlx._OIOO:Destroy() end) end
        end
        _XXlo[self._oXxo] = nil
        _lXxl = _lXxl - 1
        if _lXxl <= 0 then
            _lXxl = 0
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            _IIoO, _XXlo = nil, {}
            _oloX._XIxo("released")
        end
    end
    function _xolx.open(_oXxo)
        ensure()
        _lXxl = _lXxl + 1
        _XXlo[_oXxo] = { _llOo = 0, _OoIO = {}, _oIOx = 0, high = 0 }
        return setmetatable({ _oXxo = _oXxo }, _OxlO)
    end
    function _xolx.liveCount()
        local _oIOx = 0
        for _OXlx, _OOIX in pairs(_XXlo) do _oIOx = _oIOx + _OOIX._oIOx end
        return _oIOx
    end
    function _xolx._oxl()
        local _oIOx = 0
        for _OXlx, _OOIX in pairs(_XXlo) do
            for _OXlx in pairs(_OOIX._OoIO) do _oIOx = _oIOx + 1 end
        end
        return _oIOx
    end
    _XIxX._XXIO._lIoo("esp.cards", _xolx.liveCount)
    _XIxX._XXIO._lIoo("esp.cards.queued", _xolx._oxl)
    return _xolx
end)
_XIxX.module("features.esp.eggs", function(_XIxX)
    local _OOOX   = _XIxX.require("core.device")
    local _OOXo  = _XIxX.require("features.eggs")
    local _XIXo  = _XIxX.require("core.data")
    local _OxxO = _XIxX.require("features.esp.cards")
    local _oloX   = _XIxX.require("boot.log").for_module("esp.eggs")
    local _xolx = {}
    local _oolx = {
        REFRESH = 1.0,
        MAX_CARDS = 40,       -- a bounded pool, as V3.1 had
        LIFT_BASE = 2.2,      -- studs of clearance above the egg's centre
        LIFT_SCALE = 3.4,     -- times AssetScale, so big eggs clear their top
    }
    _xolx._oolx = _oolx
    local _lIlx, _oIoO, _olxl = nil, nil, false
    local _xOOo = { updates = 0, _IooO = 0, _llOo = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    local _xlxO, _oXlX, _lxlX, _XllX, _IxOX = _OxxO._xlxO, _OxxO._oXlX, _OxxO._lxlX, _OxxO._XllX, _OxxO._IxOX
    local function _ooIX(_oIOx)
        _oIOx = tonumber(_oIOx) or 0
        for _OXlx, _olOx in ipairs({ { 1e12, "T" }, { 1e9, "B" }, { 1e6, "M" }, { 1e3, "K" } }) do
            if _oIOx >= _olOx[1] then
                local _XlOx = _oIOx / _olOx[1]
                local _lXXX = (_XlOx < 10) and ("%.2f"):format(_XlOx) or ("%.1f"):format(_XlOx)
                return (_lXXX:gsub("%.?0+$", "")) .. _olOx[2]
            end
        end
        return tostring(math.floor(_oIOx))
    end
    local _XIlO = {}
    local _Io = Color3.fromRGB(200, 200, 200)
    local _oOlO, _XlXl = {}, {}
    local _OIXl = {}
    local function buildText(_lxlx, _oOOX)
        local _Ixlx = _lxlx.assetCategory and _oOOX and _oOOX[_lxlx.assetCategory] or nil
        local _XoOO = _Io
        local _IXX = (_lxlx._lIXO and _lxlx._lIXO ~= "?") and _lxlx._lIXO or nil
        if _Ixlx and _Ixlx.Rarity then
            if typeof(_Ixlx.Rarity.Color) == "Color3" then _XoOO = _Ixlx.Rarity.Color end
            _IXX = _IXX or _Ixlx.Rarity.DisplayName or _Ixlx.Rarity._id
        end
        local _xXoo = { _XllX(_oXlX.income, "<b>" .. _ooIX(_lxlx._XxOo or 0) .. "/s</b>") }
        if _IXX then
            _xXoo[#_xXoo + 1] = _XllX(_IxOX(_XoOO), _IXX)
        end
        local _XlIx = tonumber(_lxlx._XlIx) or 0
        if _XlIx > 0 then
            _xXoo[#_xXoo + 1] = _XllX(_oXlX.neutral,
                _XlIx >= 100 and ("%.0fkg"):format(_XlIx) or ("%.1fkg"):format(_XlIx))
        end
        local _loXX = table.concat(_xXoo, _lxlX)
        local _Illo = 1
        if type(_lxlx.mutations) == "table" and #_lxlx.mutations > 0 then
            local _Xllo = {}
            for _OXlx, mu in ipairs(_lxlx.mutations) do
                _Xllo[#_Xllo + 1] = tostring(type(mu) == "table"
                    and (mu.DisplayName or mu._id or "?") or mu)
            end
            _loXX = _loXX .. "\n" .. _XllX(_oXlX.mutation, table.concat(_Xllo, " \u{B7} "))
            _Illo = 2
        end
        return {
            _loXX = _loXX, _Illo = _Illo, _XoOO = _XoOO,
            _OIxo = _Ixlx and _Ixlx.Icon or nil,
            lift = Vector3._oooX(0, _oolx.LIFT_BASE + (tonumber(_lxlx.assetScale) or 1) * _oolx.LIFT_SCALE, 0),
        }
    end
    local function update()
        if not _olxl or not _oIoO then return end
        _xOOo.updates = _xOOo.updates + 1
        local _llOX = workspace.CurrentCamera
        local _OOxo = _OOXo._OOxo()
        if not _llOX or not _OOxo then return end
        local _oOOX = _XIXo.assetsDir()
        local _OoOX = _llOX.CFrame.Position
        for _xxlx = #_XIlO, 1, -1 do _XIlO[_xxlx] = nil end
        for _OXlx, _lxlx in ipairs(_OOxo) do
            if _lxlx._IIXX and (_lxlx._IIXX - _OoOX).Magnitude <= _OxxO._oolx.MAX_DIST then
                _XIlO[#_XIlO + 1] = _lxlx
            end
        end
        _xOOo._IooO = #_XIlO
        local _oIOx = math.min(#_XIlO, _oolx.MAX_CARDS)
        for _xxlx = 1, _oIOx do
            local _lxlx = _XIlO[_xxlx]
            local _OlOx = _oOlO[_lxlx._OXXX] or buildText(_lxlx, _oOOX)
            _XlXl[_lxlx._OXXX] = _OlOx
            local _OIlx = _OIXl[_xxlx]
            if not _OIlx then _OIlx = { _OoOo = _xlxO } _OIXl[_xxlx] = _OIlx end
            _OIlx._IIXX = _lxlx._IIXX + _OlOx.lift
            _OIlx._OXOo = _lxlx._oXxo
            _OIlx._loXX = _OlOx._loXX
            _OIlx._IIOO = _OlOx._XoOO
            _OIlx._OIxo = _OlOx._OIxo
            _OIlx._Illo = _OlOx._Illo
            _OIlx._xXXO = _lxlx.isTarget
            _oIoO:_XxIX(_xxlx, _OIlx)
        end
        _oOlO, _XlXl = _XlXl, _oOlO
        table._lIIo(_XlXl)
        _oIoO:_llOo(_oIOx)
        _xOOo._llOo = _oIOx
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        _olxl = _IoIx
        if not _IoIx then
            if _oIoO then _oIoO:close() _oIoO = nil end
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            table._lIIo(_oOlO)
            table._lIIo(_OIXl)
            _oloX._XIxo("off")
            return true
        end
        _oIoO = _OxxO.open("eggs")
        _lIlx = _XIxX.scope("features.esp.eggs")
        _lIlx:loop("update", _OOOX._oIOo(_oolx.REFRESH), update)
        _oloX._XIxo("on (max %d cards, %.2fs, range %d)",
            _oolx.MAX_CARDS, _OOOX._oIOo(_oolx.REFRESH), _OxxO._oolx.MAX_DIST)
        return true
    end
    return _xolx
end)
_XIxX.module("features.esp.plot", function(_XIxX)
    local _OoXX   = _XIxX.require("core.services")
    local _OOOX   = _XIxX.require("core.device")
    local _lXxX    = _XIxX.require("core.character")
    local _XIXo  = _XIxX.require("core.data")
    local _lolX  = _XIxX.require("core.util")
    local _OOXo  = _XIxX.require("features.eggs")
    local _OxxO = _XIxX.require("features.esp.cards")
    local _oloX   = _XIxX.require("boot.log").for_module("esp.plot")
    local _xolx = {}
    local _oolx = { RATE = 1.0, MAX_CARDS = 24, OWNER_TTL = 10 }
    _xolx._oolx = _oolx
    local _xlxO, _oXlX, _lxlX, _XllX, _IxOX = _OxxO._xlxO, _OxxO._oXlX, _OxxO._lxlX, _OxxO._XllX, _OxxO._IxOX
    local _lIlx, _oIoO, _olxl = nil, nil, false
    local _xOOo = { updates = 0, _OOXo = 0, _Xxlo = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    local function timeLeft(_xIlO)
        _xIlO = math._IOoX(0, math.floor(_xIlO))
        local _Xxlx = math.floor(_xIlO / 3600)
        local _OIOx = math.floor(_xIlO / 60) % 60
        if _Xxlx > 0 then return ("%dh %02dm"):format(_Xxlx, _OIOx) end
        if _OIOx > 0 then return ("%dm %02ds"):format(_OIOx, _xIlO % 60) end
        return ("%ds"):format(_xIlO)
    end
    local _XoIX, _xIXO, _olll = nil, 0, true
    local _Ooll = {}
    local _OIXl = {}
    local _Io = Color3.fromRGB(190, 190, 200)
    local _Xoo = _XllX(_oXlX._Xxlo, "<b>READY</b>")
    local function ownerRecords(_xIxX, _OOIx)
        local _XooX = _loIx.clock()
        if _XoIX and not _olll and (_XooX - _xIXO) < _oolx.OWNER_TTL then return _XoIX end
        local _xOIx, _OXOX = pcall(function() return _xIxX and _xIxX.ReadOwnerEggs and _xIxX.ReadOwnerEggs(_OOIx) end)
        _XoIX = (_xOIx and type(_OXOX) == "table") and _OXOX or {}
        _xIXO, _olll = _XooX, false
        table._lIIo(_Ooll)
        _xOOo.ownerReads = (_xOOo.ownerReads or 0) + 1
        return _XoIX
    end
    local function buildStatic(_OXXX, _XIXX, _oOOX)
        local _Ixlx = _XIXX and _oOOX and _oOOX[_XIXX.AssetCategory] or nil
        local _OXOo = (_Ixlx and _Ixlx.DisplayName ~= "" and _Ixlx.DisplayName)
            or (_XIXX and tostring(_XIXX.AssetCategory)) or "Egg"
        local _lIXO = _Ixlx and _Ixlx.Rarity
            and tostring(_Ixlx.Rarity.DisplayName or _Ixlx.Rarity._id or "") or ""
        local _XoOO = (_Ixlx and _Ixlx.Rarity and typeof(_Ixlx.Rarity.Color) == "Color3")
            and _Ixlx.Rarity.Color or _Io
        local _OXxo = ""
        if _XIXX and type(_XIXX.Mutations) == "table" and #_XIXX.Mutations > 0 then
            local _Xllo = {}
            for _OXlx, mu in ipairs(_XIXX.Mutations) do
                _Xllo[#_Xllo + 1] = tostring(type(mu) == "table"
                    and (mu.DisplayName or mu._id or "?") or mu)
            end
            _OXxo = table.concat(_Xllo, " \u{B7} ")
        end
        local _ooIX = nil
        if _XIXX then
            local _xOIx, _XlOx = pcall(_OOXo._XxOo, {
                Uid = _OXXX,
                AssetCategory = _XIXX.AssetCategory,
                AssetScale = _XIXX.AssetScale,
                Mutations = _XIXX.Mutations,
            })
            if _xOIx then _ooIX = _XlOx end
        end
        local _XlIx = _Ixlx and _Ixlx.Egg and tonumber(_Ixlx.Egg.WeightKg)
        if _XlIx then _XlIx = _XlIx * (tonumber(_XIXX and _XIXX.AssetScale) or 1) end
        if _XlIx and _XlIx <= 0 then _XlIx = nil end
        local _xXoo = {}
        if _ooIX and _ooIX > 0 then
            _xXoo[#_xXoo + 1] = _XllX(_oXlX.income, "<b>" .. _OOXo.formatRate(_ooIX) .. "/s</b>")
        end
        if _lIXO ~= "" then
            _xXoo[#_xXoo + 1] = _XllX(_IxOX(_XoOO), _lIXO)
        end
        if _XlIx then
            _xXoo[#_xXoo + 1] = _XllX(_oXlX.neutral, _XlIx >= 100
                and ("%.0fkg"):format(_XlIx) or ("%.1fkg"):format(_XlIx))
        end
        local _oXXo = _Ixlx and _Ixlx.Egg and tonumber(_Ixlx.Egg.GrowthTime)
        local _XxoO = _XIXX and _XIXX.Placement and tonumber(_XIXX.Placement.PlacedAt)
        local _lXxo = math._IOoX(tonumber(_XIXX and _XIXX.GrowthSpeedMultiplier) or 1, 0.01)
        return {
            _OXOo = _OXOo, _XoOO = _XoOO, _OIxo = _Ixlx and _Ixlx.Icon or nil,
            _IxXo = table.concat(_xXoo, _lxlX) .. "\n"
                .. ((_OXxo ~= "") and (_XllX(_oXlX.mutation, _OXxo) .. _lxlX) or ""),
            readyAt = (_oXXo and _XxoO) and (_XxoO + _oXXo / _lXxo) or nil,
            hasRec = _XIXX ~= nil,
            lift = Vector3._oooX(0, 2.2 + (tonumber(_XIXX and _XIXX.AssetScale) or 1) * 3.4, 0),
        }
    end
    local function update()
        if not _olxl or not _oIoO then return end
        _xOOo.updates = _xOOo.updates + 1
        local _XXol = workspace:FindFirstChild("PlacedEggRenders")
        if not _XXol then
            _oIoO:_llOo(0)
            _xOOo._OOXo = 0
            return
        end
        local _xIxX = _XIXo.eggState()
        local _oOOX = _XIXo.assetsDir()
        local _OOIx = _OoXX.Players.LocalPlayer and _OoXX.Players.LocalPlayer.UserId
        if not _OOIx then return end
        local _xxoO = tostring(_OOIx) .. "_"
        local _IOIX = #_xxoO
        local _oolo = ownerRecords(_xIxX, _OOIx)
        local _IIIO = _xIxX and _xIxX.IsReadyToHatch
        local _lxxo = _loIx.time()
        local _oIOx, _oIXO = 0, 0
        for _OXlx, _OIOx in ipairs(_XXol:GetChildren()) do
            local _oXxo = _OIOx.Name
            if string.find(_oXxo, _xxoO, 1, true) == 1 and _OIOx:IsA("Model") then
                local _OXXX = string._loXX(_oXxo, _IOIX + 1)
                local _oOlo, _OXIx = pcall(_OIOx.GetPivot, _OIOx)
                if _oOlo and _OXIx then
                    _oIOx = _oIOx + 1
                    local _llOx = _Ooll[_OXXX]
                    if not _llOx then
                        local _XIXX = _oolo[_OXXX]
                        _llOx = buildStatic(_OXXX, _XIXX, _oOOX)
                        if _XIXX then
                            _Ooll[_OXXX] = _llOx
                        else
                            _olll = true
                        end
                    end
                    local _Xxlo = false
                    if _IIIO then
                        local _oXoX, _IlOx = pcall(_IIIO, _OXXX)
                        _Xxlo = _oXoX and _IlOx == true
                    end
                    local _XOOo
                    if _Xxlo then
                        _oIXO = _oIXO + 1
                        _XOOo = _Xoo
                    elseif _llOx.readyAt then
                        _XOOo = _XllX(_oXlX.dim, timeLeft(_llOx.readyAt - _lxxo))
                    else
                        _XOOo = _XllX(_oXlX.dim, "growing")
                    end
                    local _OIlx = _OIXl[_oIOx]
                    if not _OIlx then _OIlx = { _OoOo = _xlxO, _Illo = 2 } _OIXl[_oIOx] = _OIlx end
                    _OIlx._IIXX = _OXIx.Position + _llOx.lift
                    _OIlx._OXOo = _llOx._OXOo
                    _OIlx._loXX = _llOx._IxXo .. _XOOo
                    _OIlx._IIOO = _llOx._XoOO
                    _OIlx._OIxo = _llOx._OIxo
                    _OIlx._xXXO = _Xxlo
                    _oIoO:_XxIX(_oIOx, _OIlx)
                end
            end
        end
        _oIoO:_llOo(_oIOx)
        _xOOo._OOXo, _xOOo._Xxlo = _oIOx, _oIXO
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        _olxl = _IoIx
        if not _IoIx then
            if _oIoO then _oIoO:close() _oIoO = nil end
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            _XoIX, _xIXO, _olll = nil, 0, true
            table._lIIo(_Ooll)
            table._lIIo(_OIXl)
            _oloX._XIxo("off")
            return true
        end
        _oIoO = _OxxO.open("plot")
        _lIlx = _XIxX.scope("features.esp.plot")
        _olll = true
        _XIxX.try("esp.plot.watchOwner", function()
            local _xIxX = _XIXo.eggState()
            for _OXlx, _oXxo in ipairs({ "OwnerRefreshed", "OwnerCleared" }) do
                local _lOXX = _xIxX and _xIxX[_oXxo]
                if type(_lOXX) == "table" and type(_lOXX.Connect) == "function" then
                    _lIlx:connect(_lOXX, function() _olll = true end)
                end
            end
        end)
        _lIlx:loop("update", _OOOX._oIOo(_oolx.RATE), update)
        _lXxX.onSpawn(_lIlx, "esp.plot.respawn", function()
            if _oIoO then _oIoO:_llOo(0) end
        end)
        _oloX._XIxo("on (%.2fs)", _OOOX._oIOo(_oolx.RATE))
        return true
    end
    return _xolx
end)
_XIxX.module("features.misc.servers", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _oOXo = _XIxX.require("core.exec")
    local _oloX  = _XIxX.require("boot.log").for_module("servers")
    local _xolx = {}
    local _oolx = {
        MAX_PAGES = 5, TRIES = 4,
        FAILED_FOR = 600,     -- seconds a refusal is remembered
        FAILED_MAX = 200,     -- hard ceiling; past it the oldest go first
        TP_SETTLE  = 2.5,
    }
    _xolx._oolx = _oolx
    local _OOll = false
    local _oxOO, _OOxl = {}, 0
    _XIxX._XXIO._lIoo("servers.failed", function() return _OOxl end)
    local function pruneFailed()
        local _XooX = _loIx.clock()
        local _oOxo, _oIOx = {}, 0
        for _OlIx, _oOxX in pairs(_oxOO) do
            if (_XooX - _oOxX) > _oolx.FAILED_FOR then
                _oxOO[_OlIx] = nil
            else
                _oIOx = _oIOx + 1
                _oOxo[_oIOx] = _OlIx
            end
        end
        if _oIOx > _oolx.FAILED_MAX then
            table._lIlX(_oOxo, function(_oXlx, _XXlx) return _oxOO[_oXlx] < _oxOO[_XXlx] end)
            for _xxlx = 1, _oIOx - _oolx.FAILED_MAX do
                _oxOO[_oOxo[_xxlx]] = nil
            end
            _oIOx = _oolx.FAILED_MAX
        end
        _OOxl = _oIOx
    end
    local function markFailed(_OlIx)
        if not _OlIx then return end
        _oxOO[_OlIx] = _loIx.clock()
        pruneFailed()
    end
    local function canFetch()
        if _oOXo.can._xxIO then return true end
        local _xOIx, _Oxlx = pcall(function() return game.HttpGet end)
        return _xOIx and type(_Oxlx) == "function"
    end
    local function fetchPage(_lXOO)
        local _XXXX = ("https://games.roblox.com/v1/games/%d/servers/Public"
            .. "?sortOrder=Asc&limit=100"):format(game.PlaceId)
        if _lXOO then _XXXX = _XXXX .. "&cursor=" .. tostring(_lXOO) end
        local _Ixoo, _xXXX, _IXXO
        if _oOXo.can._xxIO then
            local _OlXX
            _XIxX.try("servers.fetch", function()
                _OlXX = _oOXo.httpRequest({ Url = _XXXX, Method = "GET" })
            end)
            _Ixoo = _OlXX and (_OlXX.Body or _OlXX._Ixoo)
            _IXXO = _OlXX and (_OlXX.StatusCode or _OlXX.status_code)
            _xXXX = "request"
        end
        if not _Ixoo then
            local _xOIx, _OXOX = pcall(function() return game:HttpGet(_XXXX) end)
            if _xOIx and type(_OXOX) == "string" then _Ixoo, _xXXX = _OXOX, "HttpGet"
            elseif not _xOIx then _IXXO = tostring(_OXOX) end
        end
        if not _Ixoo then
            _oloX.warn("server list: no response (via %s, %s)", tostring(_xXXX), tostring(_IXXO))
            return nil, "no response" .. (tostring(_IXXO):find("429") and " - rate limited, wait a few seconds" or "")
        end
        local _xIxl
        pcall(function() _xIxl = _OoXX.HttpService:JSONDecode(_Ixoo) end)
        if type(_xIxl) ~= "table" or type(_xIxl._XIXo) ~= "table" then
            _oloX.warn("server list: unreadable (via %s, status %s, %d bytes: %s)",
                tostring(_xXXX), tostring(_IXXO), #_Ixoo, _Ixoo:_loXX(1, 80))
            return nil, "unreadable list"
        end
        _oloX._XIxo("server list: page via %s, %d servers%s", _xXXX, #_xIxl._XIXo,
            _xIxl.nextPageCursor and ", more pages" or "")
        return _xIxl
    end
    local function candidates()
        pruneFailed()
        local _lxoX, _lXOO = {}, nil
        local _OxXo = tostring(game.JobId)
        local _IooO, _xolo, _oxXX = 0, 0, nil
        for _OXlx = 1, _oolx.MAX_PAGES do
            local _oIIX, _loOX = fetchPage(_lXOO)
            if not _oIIX then _oxXX = _oxXX or _loOX break end
            _xolo = _xolo + 1
            for _OXlx, _Illx in ipairs(_oIIX._XIXo) do
                _IooO = _IooO + 1
                local _oXIO = tonumber(_Illx._oXIO) or 0
                local _loxo = tonumber(_Illx.maxPlayers) or 0
                if _Illx._OlIx and _Illx._OlIx ~= _OxXo             -- not the one we are in
                   and not _oxOO[_Illx._OlIx]               -- not one that refused us
                   and _loxo > 0 and _oXIO < _loxo     -- not full
                then
                    _lxoX[#_lxoX + 1] = {
                        _OlIx = _Illx._OlIx, _oXIO = _oXIO, maxPlayers = _loxo,
                        ping = tonumber(_Illx.ping) or 0,
                    }
                end
            end
            _lXOO = _oIIX.nextPageCursor
            if not _lXOO then break end
        end
        _oloX._XIxo("candidates: %d of %d listed over %d page(s) (here=%s, failed cache=%d)",
            #_lxoX, _IooO, _xolo, _OxXo:_loXX(1, 8), _OOxl)
        return _lxoX, _IooO, _oxXX
    end
    local function teleport(_Illx)
        local _llIl = nil
        local _lIXo
        pcall(function()
            _lIXo = _OoXX.TeleportService.TeleportInitFailed:Connect(function(_oxoX, _olXO, _IooX)
                if _oxoX == _OoXX.Players.LocalPlayer then
                    _llIl = tostring(_olXO) .. " " .. tostring(_IooX or "")
                end
            end)
        end)
        _oloX._XIxo("teleporting to %s (%d/%d players)", tostring(_Illx._OlIx):_loXX(1, 8),
            _Illx._oXIO, _Illx.maxPlayers)
        pcall(function() _XIxX.require("boot.log").flushNow() end)
        local _xOIx, _loOX = pcall(function()
            _OoXX.TeleportService:TeleportToPlaceInstance(game.PlaceId, _Illx._OlIx,
                _OoXX.Players.LocalPlayer)
        end)
        if _xOIx then
            local _Ollx = _loIx.clock()
            while not _llIl and (_loIx.clock() - _Ollx) < _oolx.TP_SETTLE do task.wait(0.1) end
        end
        if _lIXo then pcall(function() _lIXo:Disconnect() end) end
        if not _xOIx or _llIl then
            markFailed(_Illx._OlIx)
            _oloX.warn("teleport to %s failed: %s", tostring(_Illx._OlIx):_loXX(1, 8),
                tostring(_llIl or _loOX))
            return false, _llIl or _loOX
        end
        _oloX._XIxo("teleport requested: %s (%d/%d players)", tostring(_Illx._OlIx):_loXX(1, 8),
            _Illx._oXIO, _Illx.maxPlayers)
        return true
    end
    local function go(_Oolo, _XolX)
        if _OOll then return false, "Already searching" end
        if not canFetch() then
            _oloX.warn("%s: no HTTP capability on this executor (request=%s)", _XolX, tostring(_oOXo.can._xxIO))
            return false, "Server search is not supported by this executor"
        end
        _OOll = true
        _oloX._XIxo("%s: click", _XolX)
        local _Iolo, _xOIx, _IooX = pcall(function()
            local _OOxo, _IooO, _oxXX = candidates()
            if #_OOxo == 0 then
                if _IooO == 0 then
                    return false, "Could not read the server list" .. (_oxXX and (" (" .. _oxXX .. ")") or "")
                end
                return false, ("All %d listed servers are full or recently refused us"):format(_IooO)
            end
            table._lIlX(_OOxo, _Oolo)
            local _xIIO
            for _xxlx = 1, math.min(#_OOxo, _oolx.TRIES) do
                local _Illx = _OOxo[_xxlx]
                local _OOlX, _IxOo = teleport(_Illx)
                if _OOlX then
                    _oloX._XIxo("%s: joining %d/%d players", _XolX, _Illx._oXIO, _Illx.maxPlayers)
                    return true, ("Joining a server with %d players"):format(_Illx._oXIO)
                end
                _xIIO = _IxOo
            end
            return false, "Teleport refused " .. math.min(#_OOxo, _oolx.TRIES) .. " times"
                .. (_xIIO and (" (" .. tostring(_xIIO) .. ")") or "") .. " - press again"
        end)
        _OOll = false
        if not _Iolo then
            _oloX.warn("%s: failed: %s", _XolX, tostring(_xOIx))
            return false, "Server search failed - see the log"
        end
        return _xOIx, _IooX
    end
    function _xolx.lowestServer()
        return go(function(_oXlx, _XXlx)
            if _oXlx._oXIO ~= _XXlx._oXIO then return _oXlx._oXIO < _XXlx._oXIO end
            local _lOxX = _oXlx.ping > 0 and _oXlx.ping or math.huge
            local _OoxX = _XXlx.ping > 0 and _XXlx.ping or math.huge
            return _lOxX < _OoxX
        end, "lowest")
    end
    function _xolx.hop()
        return go(function(_oXlx, _XXlx) return _oXlx._oXIO < _XXlx._oXIO end, "hop")
    end
    function _xolx._xOOo()
        pruneFailed()
        return { failedServers = _OOxl, _OOll = _OOll }
    end
    return _xolx
end)
_XIxX.module("features.misc.webhook", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _oOXo = _XIxX.require("core.exec")
    local _lolX = _XIxX.require("core.util")
    local _oloX  = _XIxX.require("boot.log").for_module("webhook")
    local _xolx = {}
    local _oolx = { MIN_GAP = 3.0, TIMEOUT = 8 }
    _xolx._oolx = _oolx
    local _olxl = false
    local _XXXX = nil              -- never logged, never returned
    local _oOol = 0
    local _xOOo = { sent = 0, _oxOO = 0, _llxl = 0, _OllO = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    function _xolx.hasUrl() return _XXXX ~= nil and _XXXX ~= "" end
    function _xolx.redactedUrl()
        if not _xolx.hasUrl() then return "not set" end
        local _IIxo = tostring(_XXXX):match("^https?://([^/]+)") or "?"
        return ("%s/...(%d chars)"):format(_IIxo, #_XXXX)
    end
    function _xolx.setEnabled(_IoIx)
        _olxl = _IoIx and true or false
        _oloX._XIxo("%s (url %s)", _olxl and "enabled" or "disabled", _xolx.redactedUrl())
        return true
    end
    function _xolx.setUrl(_XlOx)
        _XlOx = tostring(_XlOx or ""):gsub("%s", "")
        if _XlOx == "" then
            _XXXX = nil
            _oloX._XIxo("url cleared")
            return true, "URL cleared"
        end
        if not _XlOx:match("^https://") then
            return false, "That does not look like a webhook URL"
        end
        _XXXX = _XlOx
        _oloX._XIxo("url set (%s)", _xolx.redactedUrl())
        return true, "Webhook URL saved"
    end
    local function embedFor(_lxlx)
        local _XxOO = {}
        local function add(_oXxo, _XxOo)
            if _XxOo == nil or _XxOo == "" then return end
            _XxOO[#_XxOO + 1] = { _oXxo = _oXxo, _XxOo = tostring(_XxOo), inline = true }
        end
        add("Income", (_lxlx._XxOo and (_lolX._IlOo(_lxlx._XxOo) .. "/s")) or nil)
        add("Weight", _lxlx._XlIx and _lxlx._XlIx > 0 and ("%.1f kg"):format(_lxlx._XlIx) or nil)
        add("Rarity", _lxlx._lIXO ~= "?" and _lxlx._lIXO or nil)
        add("Mutation", _lxlx.mutation)
        add("Area", _lxlx._oIOO)
        return {
            username = "RYUZAKI HUB",
            embeds = { {
                _OXOo = "Egg delivered",
                description = "**" .. tostring(_lxlx._oXxo or "Egg") .. "**",
                _oIIo = 5814783,
                _XxOO = _XxOO,
                footer = { _OllX = "RyuzakiHub " .. tostring(_XIxX.version) },
                timestamp = _loIx.date("!%Y-%m-%dT%H:%M:%SZ"),
            } },
        }
    end
    local function post(_loIO, _ooXX)
        if not _oOXo.can._xxIO then
            _xOOo._OllO = _xOOo._OllO + 1
            _oloX.warn("no HTTP request capability - nothing sent")
            return false
        end
        local _Ixoo
        local _OOlo = pcall(function() _Ixoo = _OoXX.HttpService:JSONEncode(_loIO) end)
        if not _OOlo or not _Ixoo then
            _xOOo._oxOO = _xOOo._oxOO + 1
            return false
        end
        local _OlXX
        local _xOIx = _XIxX.try("webhook.post", function()
            _OlXX = _oOXo.httpRequest({
                Url = _XXXX, Method = "POST",
                Headers = { ["Content-Type"] = "application/json" },
                Body = _Ixoo,
            })
        end)
        local _IIXo = _OlXX and (_OlXX.StatusCode or _OlXX.status_code)
        if _xOIx and _IIXo and _IIXo >= 200 and _IIXo < 300 then
            _xOOo.sent = _xOOo.sent + 1
            _oloX._XIxo("%s sent (HTTP %s)", _ooXX, tostring(_IIXo))
            return true
        end
        _xOOo._oxOO = _xOOo._oxOO + 1
        _oloX.warn("%s failed (HTTP %s)", _ooXX, tostring(_IIXo or "no response"))
        return false
    end
    function _xolx.onDelivered(_lxlx)
        if not _olxl or not _xolx.hasUrl() or type(_lxlx) ~= "table" then return end
        local _XooX = _loIx.clock()
        if _XooX - _oOol < _oolx.MIN_GAP then
            _xOOo._llxl = _xOOo._llxl + 1
            return
        end
        _oOol = _XooX
        task.spawn(function()
            _XIxX.try("webhook.delivered", function()
                post(embedFor(_lxlx), "delivery")
            end)
        end)
    end
    function _xolx.test()
        if not _xolx.hasUrl() then return false, "Set a webhook URL first" end
        task.spawn(function()
            _XIxX.try("webhook.test", function()
                post({
                    username = "RYUZAKI HUB",
                    embeds = { {
                        _OXOo = "Test",
                        description = "Webhook is working.",
                        _oIIo = 5814783,
                        footer = { _OllX = "RyuzakiHub " .. tostring(_XIxX.version) },
                        timestamp = _loIx.date("!%Y-%m-%dT%H:%M:%SZ"),
                    } },
                }, "test")
            end)
        end)
        return true, "Test sent"
    end
    return _xolx
end)
_XIxX.module("features.misc.appearance", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _XxXX = _XIxX.require("ui.window")
    local _oloX = _XIxX.require("boot.log").for_module("appearance")
    local _xolx = {}
    local _oolx = { FADE = 0.35, CORNER = 12 }
    _xolx._oolx = _oolx
    local _lIlx = nil
    local _oIxl = { theme = nil, background = nil }
    local function themeApi()
        local _IloX = _XxXX._IloX
        if type(_IloX) == "table" then
            for _OXlx, _oXxo in ipairs({ "SetTheme", "ChangeTheme", "ApplyTheme" }) do
                if type(_IloX[_oXxo]) == "function" then
                    return function(_XlOx) _IloX[_oXxo](_IloX, _XlOx) end, _oXxo
                end
            end
        end
        local _xlOx = _XxXX.window
        if type(_xlOx) == "table" then
            for _OXlx, _oXxo in ipairs({ "SetTheme", "ChangeTheme" }) do
                if type(_xlOx[_oXxo]) == "function" then
                    return function(_XlOx) _xlOx[_oXxo](_xlOx, _XlOx) end, _oXxo
                end
            end
        end
        return nil
    end
    function _xolx.themeSupported() return (themeApi()) ~= nil end
    function _xolx.themes()
        local _IloX = _XxXX._IloX
        local _Xllo = {}
        if type(_IloX) == "table" and type(_IloX.Theme) == "table" then
            for _IIOx in pairs(_IloX.Theme) do _Xllo[#_Xllo + 1] = tostring(_IIOx) end
        end
        if #_Xllo == 0 then
            _Xllo = { "Default", "Amethyst", "Green", "Bloom", "DarkBlue",
                      "Light", "Serenity" }
        end
        table._lIlX(_Xllo)
        return _Xllo
    end
    function _xolx.setTheme(_oXxo)
        _oXxo = tostring(_oXxo or "")
        if _oXxo == "" then return false, "Pick a theme" end
        local _OoxO, _xXXX = themeApi()
        if not _OoxO then
            _oloX.warn("direct UI has no external theme API")
            return false, "This menu build has no theme support"
        end
        if not _XIxX.try("appearance.setTheme", function() _OoxO(_oXxo) end) then
            return false, "That theme was refused"
        end
        _oIxl.theme = _oXxo
        _oloX._XIxo("theme set to %s (via %s)", _oXxo, tostring(_xXXX))
        return true, "Theme: " .. _oXxo
    end
    local _OxXl, _lOll, _oOIl = nil, nil, nil
    local _xxIO = 0        -- a newer id cancels any pending retry or loader
    local function restoreWindowFill()
        if _oOIl then
            pcall(function() _oOIl:Disconnect() end)
            _oOIl = nil
        end
        if _OxXl and _lOll ~= nil then
            pcall(function()
                local _IIxo = _OxXl.Parent
                if _IIxo then _IIxo.BackgroundTransparency = _lOll end
            end)
        end
        _lOll = nil
    end
    local function findHost()
        local _oXOX = _XxXX.screen
        if not _oXOX or not _oXOX.Parent then return nil end
        local _oXoo, _oOOl
        for _OXlx, _Oxlx in ipairs(_oXOX:GetChildren()) do
            if _Oxlx:IsA("Frame") and _Oxlx.Visible then
                local _oXlx = _Oxlx.AbsoluteSize.X * _Oxlx.AbsoluteSize.Y
                if not _oOOl or _oXlx > _oOOl then _oXoo, _oOOl = _Oxlx, _oXlx end
            end
        end
        return _oXoo
    end
    local function applyBackground(_OlIx)
        restoreWindowFill()
        if _OxXl then pcall(function() _OxXl:Destroy() end) end
        _OxXl = nil
        _OlIx = tostring(_OlIx or ""):gsub("%s", "")
        if _OlIx == "" then
            _oIxl.background = nil
            local _XXoo = _XIxX._scopes["features.misc.appearance.background"]
            if _XXoo and not _XXoo._xIXo then _XXoo:destroy() end
            return true, "cleared"
        end
        if not _OlIx:match("^%d+$") then
            _OlIx = _OlIx:match("(%d+)") or ""
            if _OlIx == "" then return false, "that is not an image id" end
        end
        local _IIxo = findHost()
        if not _IIxo then return false, "could not find the hub window" end
        local _XXoo = _XIxX.scope("features.misc.appearance.background")
        local _OIoX = Instance._oooX("ImageLabel")
        _OIoX.Name = "RyuzakiBackground"
        _OIoX.Size = UDim2.fromScale(1, 1)
        _OIoX.Image = "rbxassetid://" .. _OlIx
        _OIoX.ScaleType = Enum.ScaleType.Crop
        _OIoX.ImageTransparency = _oolx.FADE
        _OIoX.BackgroundColor3 = Color3.fromRGB(16, 16, 20)
        _OIoX.BackgroundTransparency = 0
        _OIoX.BorderSizePixel = 0
        _OIoX.ZIndex = 0
        Instance._oooX("UICorner", _OIoX).CornerRadius = UDim._oooX(0, 0)
        _XXoo:own(_OIoX)
        _OIoX.Parent = _IIxo
        _lOll = _IIxo.BackgroundTransparency
        _IIxo.BackgroundTransparency = 1
        _OxXl = _OIoX
        _oIxl.background = _OlIx
        _oOIl = _XXoo:connect(_IIxo:GetPropertyChangedSignal("BackgroundTransparency"),
            function()
                if _OxXl == _OIoX and _OIoX.Parent == _IIxo
                   and _IIxo.BackgroundTransparency ~= 1 then
                    _lOll = _IIxo.BackgroundTransparency
                    _IIxo.BackgroundTransparency = 1
                end
            end)
        local _Ooxo = _xxIO
        _XXoo:spawn("bgLoad", function()
            for _OXlx = 1, 5 do
                task.wait(0.2)
                if _OIoX.Parent == nil or _xxIO ~= _Ooxo then return end
                if _OIoX.IsLoaded then _oloX._XIxo("background loaded directly") return end
            end
            if _OIoX.Parent == nil or _xxIO ~= _Ooxo then return end
            _OIoX.Image = ("rbxthumb://type=Asset&id=%s&w=420&h=420"):format(_OlIx)
            for _OXlx = 1, 25 do
                task.wait(0.2)
                if _OIoX.Parent == nil or _xxIO ~= _Ooxo then return end
                if _OIoX.IsLoaded then
                    _oloX._XIxo("background loaded through the thumbnail endpoint")
                    return
                end
            end
            if _OIoX.Parent then
                _oloX.warn("id %s would not load either way", _OlIx)
                _XIxX.try("appearance.bgNotify", function()
                    _XxXX.notify("Appearance", "Roblox will not serve that id as an image", 4)
                end)
            end
        end)
        return true, "applied"
    end
    function _xolx.setBackground(_OlIx)
        _xxIO = _xxIO + 1
        local _Ooxo = _xxIO
        local _xOIx, _oxXX = applyBackground(_OlIx)
        if not _xOIx and tostring(_oxXX):find("could not find the hub window") then
            _lIlx = _lIlx or _XIxX.scope("features.misc.appearance")
            _lIlx:spawn("bgWait", function()
                for _OXlx = 1, 60 do
                    task.wait(0.5)
                    if _xxIO ~= _Ooxo then return end
                    local _lXoX, _xolX = applyBackground(_OlIx)
                    if _lXoX or not tostring(_xolX):find("could not find the hub window") then
                        _oloX._XIxo("background: %s (once the window was up)", tostring(_xolX))
                        return
                    end
                end
                _oloX.warn("gave up - the hub window never appeared")
            end)
            return true, "Waiting for the window"
        end
        if _xOIx then _oloX._XIxo("background %s (id %s)", _oxXX, tostring(_OlIx)) end
        return _xOIx, _xOIx and ("Background " .. _oxXX) or ("Background failed - " .. _oxXX)
    end
    function _xolx.clearBackground()
        _xxIO = _xxIO + 1
        applyBackground("")
        return true, "Background cleared"
    end
    function _xolx.currentBackground() return _oIxl.background end
    function _xolx.read()
        return { theme = _oIxl.theme, background = _oIxl.background }
    end
    function _xolx._OoxO(_OlOx)
        if type(_OlOx) ~= "table" then return end
        if _OlOx.theme then _xolx.setTheme(_OlOx.theme) end
        if _OlOx.background and tostring(_OlOx.background) ~= "" then
            _xolx.setBackground(_OlOx.background)
        end
    end
    function _xolx.reset()
        restoreWindowFill()
        if _lIlx then _lIlx:destroy() _lIlx = nil end
        _OxXl, _oOIl = nil, nil
        _oIxl = { theme = nil, background = nil }
    end
    return _xolx
end)
_XIxX.module("features.gamethrottle", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _xIlx   = _XIxX.require("core.state")
    local _oOXo = _XIxX.require("core.exec")
    local _oloX  = _XIxX.require("boot.log").for_module("gamethrottle")
    local _xolx = {}
    local _oolx = {
        PETS_HZ    = 30,
        PROMPTS_HZ = 10,
    }
    _xolx._oolx = _oolx
    local _IoOX = (type(getgenv) == "function" and getgenv()) or _G
    local _xOXl = "__RYUZAKI_THROTTLE"
    local _olxl = false
    local _xOOo = { _llIX = false, _xXIO = false, petSteps = 0, petSkips = 0,
                    promptSteps = 0, promptSkips = 0 }
    function _xolx.isOn() return _olxl end
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    local function petsClass()
        local _XOoX
        pcall(function()
            _XOoX = _OoXX.Players.LocalPlayer.PlayerScripts.Game.Plots
                .ActiveAssetsController.AssetMovementBatch
        end)
        if not (_XOoX and _XOoX:IsA("ModuleScript")) then return nil end
        local _xOIx, _xlOX = pcall(require, _XOoX)
        if _xOIx and type(_xlOX) == "table" and type(rawget(_xlOX, "_step")) == "function" then
            return _xlOX
        end
        return nil
    end
    local function followerAdvance()
        local _OIoO = (debug and debug.getupvalues) or rawget(_IoOX, "getupvalues")
        if type(_OIoO) ~= "function" then return nil end
        local _XOoX = _OoXX.ReplicatedStorage:FindFirstChild("Client")
        _XOoX = _XOoX and _XOoX:FindFirstChild("SmartProximityPrompt")
        _XOoX = _XOoX and _XOoX:FindFirstChild("FollowerLoop")
        if not (_XOoX and _XOoX:IsA("ModuleScript")) then return nil end
        local _xOIx, _IloX = pcall(require, _XOoX)
        if not _xOIx or type(_IloX) ~= "table" or type(_IloX.Add) ~= "function" then return nil end
        local _XXoX, _oXXX = pcall(_OIoO, _IloX.Add)
        if not _XXoX or type(_oXXX) ~= "table" then return nil end
        for _OXlx, _olOx in pairs(_oXXX) do
            if type(_olOx) == "function" then
                local _OXoX, _oXxo = pcall(debug._XIxo, _olOx, "n")
                if _OXoX and _oXxo == "advance" then return _olOx end
            end
        end
        return nil
    end
    local function restore(_XIXX, _oxXX)
        if type(_XIXX) ~= "table" then return end
        if _XIXX._xlOX and _XIXX._oIlX then
            pcall(rawset, _XIXX._xlOX, "_step", _XIXX._oIlX)
        end
        if _XIXX._ooXl and _XIXX.advanceOrig and type(hookfunction) == "function" then
            pcall(hookfunction, _XIXX._ooXl, _XIXX.advanceOrig)
        end
        _oloX._XIxo("restored game loops (%s)", tostring(_oxXX))
    end
    if type(_IoOX[_xOXl]) == "table" then
        local _lOOo = _IoOX[_xOXl]
        _IoOX[_xOXl] = nil
        _XIxX.try("throttle.restoreStale", restore, _lOOo, "previous copy")
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        if not _IoIx then
            _olxl = false
            restore(_IoOX[_xOXl], "toggled off")
            _IoOX[_xOXl] = nil
            _xOOo._llIX, _xOOo._xXIO = false, false
            return true
        end
        _olxl = true
        local _XIXX = {}
        _IoOX[_xOXl] = _XIXX
        _XIxX.try("throttle.pets", function()
            local _xlOX = petsClass()
            if not _xlOX then _oloX._XIxo("pet movement batch not found - left alone") return end
            local _xxxo = rawget(_xlOX, "_step")
            local _lxoO = 1 / _oolx.PETS_HZ
            local _XxlX = setmetatable({}, { __mode = "k" })
            _XIXX._xlOX, _XIXX._oIlX = _xlOX, _xxxo
            rawset(_xlOX, "_step", function(self, _xXxX)
                local _oXlx = (_XxlX[self] or 0) + (tonumber(_xXxX) or 0)
                if _oXlx < _lxoO then
                    _XxlX[self] = _oXlx
                    _xOOo.petSkips = _xOOo.petSkips + 1
                    return
                end
                _XxlX[self] = 0
                _xOOo.petSteps = _xOOo.petSteps + 1
                return _xxxo(self, _oXlx)
            end)
            _xOOo._llIX = true
        end)
        _XIxX.try("throttle.prompts", function()
            if not _oOXo.can.hooking or type(hookfunction) ~= "function" then
                _oloX._XIxo("no hookfunction - prompt follower left alone")
                return
            end
            local _ooXl = followerAdvance()
            if not _ooXl then _oloX._XIxo("prompt follower not found - left alone") return end
            local _lxoO = 1 / _oolx.PROMPTS_HZ
            local _XxlX = 0
            local _xxxo
            local function throttled(_xXxX)
                _xXxX = tonumber(_xXxX) or 0
                if _xIlx.autoStealOn then
                    _XxlX = 0
                    return _xxxo(_xXxX)
                end
                _XxlX = _XxlX + _xXxX
                if _XxlX < _lxoO then
                    _xOOo.promptSkips = _xOOo.promptSkips + 1
                    return
                end
                local _Ixlx = _XxlX
                _XxlX = 0
                _xOOo.promptSteps = _xOOo.promptSteps + 1
                return _xxxo(_Ixlx)
            end
            _xxxo = hookfunction(_ooXl, throttled)
            _XIXX._ooXl, _XIXX.advanceOrig = _ooXl, _xxxo
            _xOOo._xXIO = true
        end)
        _oloX._XIxo("on (pets %s @%dHz, prompts %s @%dHz)",
            tostring(_xOOo._llIX), _oolx.PETS_HZ, tostring(_xOOo._xXIO), _oolx.PROMPTS_HZ)
        return true
    end
    return _xolx
end)
_XIxX.module("features.fps", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _oloX = _XIxX.require("boot.log").for_module("fps")
    local _xolx = {}
    local _oolx = {
        MAX_TRACKED = 4000,   -- ceiling on remembered effects (403 live today)
        CHUNK       = 1200,   -- descendants examined between yields
        PRUNE_EVERY = 30,     -- seconds between destroyed-instance sweeps
        DEFER       = 2.0,    -- seconds after startup before the first apply
    }
    _xolx._oolx = _oolx
    local _oOXl = {
        ParticleEmitter = true, Trail = true, Beam = true,
        Smoke = true, Fire = true, Sparkles = true,
    }
    local _Xloo = {
        BloomEffect = true, BlurEffect = true, ColorCorrectionEffect = true,
        SunRaysEffect = true, DepthOfFieldEffect = true,
    }
    local _IoOX = (type(getgenv) == "function" and getgenv()) or _G
    local _xOXl = "__RYUZAKI_FPS"
    local function newRecord()
        return { _Oxlo = {}, _oIOx = 0 }
    end
    local function restoreRecord(_XIXX, _oxXX)
        if type(_XIXX) ~= "table" or type(_XIXX._Oxlo) ~= "table" then return 0 end
        local _OIXX = 0
        for _xxlx = #_XIXX._Oxlo, 1, -1 do
            local _lxlx = _XIXX._Oxlo[_xxlx]
            if _lxlx and _lxlx._IXoX then
                local _xOIx = pcall(function() _lxlx._IXoX[_lxlx._xIoX] = _lxlx._lxXX end)
                if _xOIx then _OIXX = _OIXX + 1 end
            end
            _XIXX._Oxlo[_xxlx] = nil
        end
        _XIXX._oIOx = 0
        _oloX._XIxo("restored %d properties (%s)", _OIXX, tostring(_oxXX))
        return _OIXX
    end
    if type(_IoOX[_xOXl]) == "table" then
        local _lOOo = _IoOX[_xOXl]
        _IoOX[_xOXl] = nil
        _XIxX.try("fps.restoreStale", function()
            restoreRecord(_lOOo, "previous copy, before re-applying")
        end)
    end
    _XIxX.try("fps.throttleStale", function() _XIxX.require("features.gamethrottle") end)
    local _lIlx, _XIXX, _olxl, _llXl = nil, nil, false, false
    local _xOOo = { effects = 0, _Oxlo = 0, added = 0, pruned = 0, refused = 0,
                    sweepMs = 0 }
    function _xolx.isOn() return _olxl end
    function _xolx._xOOo()
        local _llOx = table._OIIo(_xOOo)
        _llOx.tracked = _XIXX and _XIXX._oIOx or 0
        return _llOx
    end
    _XIxX._XXIO._lIoo("fps.tracked", function() return _XIXX and _XIXX._oIOx or 0 end)
    local function remember(_IXoX, _xIoX, _XxOo)
        if not _XIXX then return false end
        if _XIXX._oIOx >= _oolx.MAX_TRACKED then
            _xOOo.refused = _xOOo.refused + 1
            if _xOOo.refused == 1 then
                _oloX.warn("tracking ceiling of %d reached - further effects left as they are",
                    _oolx.MAX_TRACKED)
            end
            return false
        end
        local _lxXX
        if not pcall(function() _lxXX = _IXoX[_xIoX] end) then return false end
        if _lxXX == _XxOo then return false end      -- nothing to change, nothing to remember
        if not pcall(function() _IXoX[_xIoX] = _XxOo end) then return false end
        _XIXX._oIOx = _XIXX._oIOx + 1
        _XIXX._Oxlo[_XIXX._oIOx] = { _IXoX = _IXoX, _xIoX = _xIoX, _lxXX = _lxXX }
        return true
    end
    local function offLimits(_Ixlx)
        local _xlxl = workspace:FindFirstChild("RyuzakiESP")
        if _xlxl and _Ixlx:IsDescendantOf(_xlxl) then return true end
        local _xxoo = _OoXX.Players.LocalPlayer and _OoXX.Players.LocalPlayer.Character
        if _xxoo and _Ixlx:IsDescendantOf(_xxoo) then return true end
        return false
    end
    local function _oIoO(_Ixlx)
        local _xlOX = _Ixlx.ClassName
        if not (_oOXl[_xlOX] or _Xloo[_xlOX]) then return false end
        if _oOXl[_xlOX] and offLimits(_Ixlx) then return false end
        if remember(_Ixlx, "Enabled", false) then
            _xOOo.effects = _xOOo.effects + 1
            return true
        end
        return false
    end
    local function sweep()
        if _llXl then return end
        _llXl = true
        local _Ollx = _loIx.clock()
        for _OXlx, _Ixlx in ipairs(_OoXX.Lighting:GetDescendants()) do
            _XIxX.try("fps.sweepPost", _oIoO, _Ixlx)
        end
        local _llXo = workspace:GetDescendants()
        local _XXOo = #_llXo
        local _xxlx = 1
        while _xxlx <= _XXOo do
            local _XIlX = math.min(_xxlx + _oolx.CHUNK - 1, _XXOo)
            for j = _xxlx, _XIlX do
                local _Ixlx = _llXo[j]
                if _Ixlx then _XIxX.try("fps.sweepOne", _oIoO, _Ixlx) end
            end
            _xxlx = _XIlX + 1
            _OoXX.RunService.Heartbeat:Wait()
            if not _olxl or not (_lIlx and _lIlx:alive()) then break end
        end
        _xOOo.sweepMs = (_loIx.clock() - _Ollx) * 1000
        _llXl = false
        _oloX._XIxo("sweep: %d descendants, %d effects off, %.1fms",
            _XXOo, _xOOo.effects, _xOOo.sweepMs)
    end
    local function applyGlobals()
        remember(_OoXX.Lighting, "GlobalShadows", false)
        local _XoXX = workspace:FindFirstChildOfClass("Terrain")
        if _XoXX then
            remember(_XoXX, "Decoration", false)
            remember(_XoXX, "WaterWaveSize", 0)
            remember(_XoXX, "WaterWaveSpeed", 0)
            remember(_XoXX, "WaterReflectance", 0)
        end
        _XIxX.try("fps.quality", function()
            local _IlOx = settings().Rendering
            remember(_IlOx, "QualityLevel", Enum.QualityLevel.Level01)
        end)
        _xOOo._Oxlo = _XIXX and _XIXX._oIOx or 0
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        _olxl = _IoIx
        if not _IoIx then
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            _XIxX.try("fps.throttleOff", function()
                _XIxX.require("features.gamethrottle").setEnabled(false)
            end)
            local _OIXX = restoreRecord(_XIXX, "toggled off")
            _XIXX = nil
            _IoOX[_xOXl] = nil
            _xOOo.effects, _xOOo._Oxlo = 0, 0
            _oloX._XIxo("off (%d properties restored)", _OIXX)
            return true
        end
        _XIXX = newRecord()
        _IoOX[_xOXl] = _XIXX
        _lIlx = _XIxX.scope("features.fps")
        applyGlobals()
        _XIxX.try("fps.throttleOn", function()
            _XIxX.require("features.gamethrottle").setEnabled(true)
        end)
        _lIlx:spawn("sweep", sweep)
        _lIlx:connect(workspace.DescendantAdded, _XIxX._lXIo("fps.added", function(_Ixlx)
            if not _olxl then return end
            if _oIoO(_Ixlx) then _xOOo.added = _xOOo.added + 1 end
        end))
        _lIlx:connect(_OoXX.Lighting.DescendantAdded, _XIxX._lXIo("fps.addedPost", function(_Ixlx)
            if not _olxl then return end
            if _oIoO(_Ixlx) then _xOOo.added = _xOOo.added + 1 end
        end))
        _lIlx:loop("prune", _oolx.PRUNE_EVERY, function()
            if not _XIXX then return end
            local _Oxlo, _llxo = _XIXX._Oxlo, 0
            local _llxl = 0
            for _xxlx = 1, _XIXX._oIOx do
                local _lxlx = _Oxlo[_xxlx]
                local _IXXo = false
                if _lxlx and _lxlx._IXoX then
                    if typeof(_lxlx._IXoX) == "Instance" and _lxlx._IXoX.Parent == nil then
                        _IXXo = true
                    end
                else
                    _IXXo = true
                end
                if _IXXo then
                    _llxl = _llxl + 1
                else
                    _llxo = _llxo + 1
                    _Oxlo[_llxo] = _lxlx
                end
            end
            for _xxlx = _llxo + 1, _XIXX._oIOx do _Oxlo[_xxlx] = nil end
            _XIXX._oIOx = _llxo
            if _llxl > 0 then
                _xOOo.pruned = _xOOo.pruned + _llxl
                _oloX.trace("pruned %d destroyed effects (%d tracked)", _llxl, _llxo)
            end
        end)
        _oloX._XIxo("on")
        return true
    end
    _XIxX.onTeardown("fps", function() _xolx.setEnabled(false) end)
    local _XoxO = false
    function _xolx.arm()
        if _XoxO then return false end
        _XoxO = true
        task.delay(_oolx.DEFER, function()
            if not _XIxX.alive() then return end
            if _olxl then return end
            if _xolx.userTurnedOff then return end
            _XIxX.try("fps.armApply", function() _xolx.setEnabled(true) end)
        end)
        return true
    end
    return _xolx
end)
_XIxX.module("features.boss", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _OOOX = _XIxX.require("core.device")
    local _OooX = _XIxX.require("core.net")
    local _oloX = _XIxX.require("boot.log").for_module("boss")
    local _xolx = {}
    local _oolx = {
        SNAP_TTL  = 5,
        BACKSTOP  = 30,
        ENTER_GAP = 1.0,
        RETRY     = { 5, 10, 20 },
    }
    _xolx._oolx = _oolx
    local _lIlx, _olxl = nil, false
    local _IIlX, _loXO = nil, 0
    local _XlXO, _lxX = 0, false
    local _lXx = false
    local _xOOo = { asks = 0, enters = 0, entersRefused = 0, _ooOO = 0,
                    stateEvents = 0, autoEntered = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    function _xolx.autoEnterOn() return _lXx end
    local _xXIl = {}
    function _xolx.onChange(_xxxX) _xXIl[#_xXIl + 1] = _xxxX end
    local function fireChange()
        for _OXlx, _xxxX in ipairs(_xXIl) do
            task.spawn(function() _XIxX.try("boss.onChange", _xxxX) end)
        end
    end
    function _xolx.snapshot(_loIo)
        if not _olxl then return nil end
        local _XooX = _loIx.clock()
        if not _loIo and _IIlX and (_XooX - _loXO) < _oolx.SNAP_TTL then return _IIlX end
        _xOOo.asks = _xOOo.asks + 1
        local _xIlx = _OooX.call("RF/BossEvent/AskSnapshot")
        _loXO = _XooX
        if type(_xIlx) == "table" then _IIlX = _xIlx end
        return _IIlX
    end
    function _xolx._IOoO()
        local _llOx = _xolx.snapshot()
        return (_llOx and _llOx.Open == true) or false
    end
    function _xolx._lxXo() return _IIlX end
    local function clock(_xIlO)
        _xIlO = math._IOoX(0, math.floor(_xIlO or 0))
        local _Xxlx = math.floor(_xIlO / 3600)
        local _OIOx = math.floor(_xIlO / 60) % 60
        if _Xxlx > 0 then return ("%dh %02dm"):format(_Xxlx, _OIOx) end
        if _OIOx > 0 then return ("%dm %02ds"):format(_OIOx, _xIlO % 60) end
        return ("%ds"):format(_xIlO)
    end
    function _xolx._IXXO()
        if not _olxl then return { _OXOo = "Abyss Overlord", _Ixoo = "off" } end
        local _llOx = _IIlX
        if not _llOx then
            return { _OXOo = "Abyss Overlord", _Ixoo = (_xOOo.asks > 0)
                and "Unavailable  \u{B7}  retrying"
                or "Reading..." }
        end
        local _lXoO = workspace:GetServerTimeNow()
        if _llOx.Open == true then
            local _IOxo = (tonumber(_llOx.ClosesAt) or 0) - _lXoO
            return { _OXOo = "Abyss Overlord",
                     _Ixoo = ("OPEN  \u{B7}  closes in %s"):format(clock(_IOxo)) }
        end
        local _oxXO = (tonumber(_llOx.OpensAt) or 0) - _lXoO
        if _oxXO > 0 then
            return { _OXOo = "Abyss Overlord",
                     _Ixoo = ("Closed  \u{B7}  opens in %s"):format(clock(_oxXO)) }
        end
        return { _OXOo = "Abyss Overlord", _Ixoo = "Closed" }
    end
    function _xolx._oxIO()
        if not _olxl then return false end
        task.spawn(function()
            _XIxX.try("boss.refresh", function()
                _xolx.snapshot(true)
                fireChange()
            end)
        end)
        return true
    end
    local function readOrRetry()
        local _xIlx = _xolx.snapshot(true)
        if _xIlx then
            _XlXO = 0
            return _xIlx
        end
        if _lxX or not _lIlx then return nil end
        local wait = _oolx.RETRY[_XlXO + 1]
        if not wait then return nil end
        _lxX = true
        _oloX.warn("boss read failed - retrying in %ds", wait)
        _lIlx:delay("retry", _OOOX._oIOo(wait), function()
            _lxX = false
            _XlXO = _XlXO + 1
            if readOrRetry() then fireChange() end
        end)
        return nil
    end
    function _xolx.enter()
        _xOOo.enters = _xOOo.enters + 1
        local _IlOl, _IooX = _OooX.call("RF/BossEvent/AskEnter")
        _oloX._XIxo("AskEnter -> accepted=%s msg=%s", tostring(_IlOl), tostring(_IooX))
        if _IlOl == true then
            return true, "Entering the boss world"
        end
        _xOOo.entersRefused = _xOOo.entersRefused + 1
        if _IooX and tostring(_IooX):find("defeated") then
            return false, "Boss already defeated - waiting for the next one"
        end
        return false, tostring(_IooX or "Refused")
    end
    function _xolx.setAutoEnter(_IoIx)
        _lXx = _IoIx and true or false
        _oloX._XIxo("auto enter %s", _lXx and "ON" or "OFF")
        if _lXx and _olxl and _xolx._IOoO() then
            task.spawn(function()
                _XIxX.try("boss.autoEnterNow", function()
                    local _xOIx, _oxXX = _xolx.enter()
                    if _xOIx then _xOOo.autoEntered = _xOOo.autoEntered + 1 end
                    _oloX._XIxo("auto enter (already open) -> %s %s", tostring(_xOIx), tostring(_oxXX))
                end)
            end)
        end
        return true
    end
    function _xolx.claimMilestones()
        local _oIxX
        local _xOlo = _XIxX.try("boss.requireMastery", function()
            local _XOoX = _OoXX.ReplicatedStorage:FindFirstChild("Data")
            _XOoX = _XOoX and _XOoX:FindFirstChild("BossMastery")
            if _XOoX and _XOoX:IsA("ModuleScript") then _oIxX = require(_XOoX) end
        end)
        if not _xOlo or type(_oIxX) ~= "table" then
            _oloX.warn("Data.BossMastery unavailable - cannot claim")
            return 0, "Could not read the mastery list"
        end
        local _lIoX = {}
        for _OXlx, _OIOx in pairs(_oIxX.Milestones or {}) do
            if type(_OIOx) == "table" and _OIOx.Id then _lIoX[#_lIoX + 1] = tostring(_OIOx.Id) end
        end
        if _oIxX.InfiniteMilestoneId then _lIoX[#_lIoX + 1] = tostring(_oIxX.InfiniteMilestoneId) end
        local _IIxl = 0
        for _OXlx, _OlIx in ipairs(_lIoX) do
            local _OXOX, _IooX = _OooX.call("RF/BossMastery/AskClaimMilestone", _OlIx)
            if _OXOX == true then
                _IIxl = _IIxl + 1
                _oloX._XIxo("claimed milestone %s", _OlIx)
            elseif _IooX and not tostring(_IooX):find("Not enough") then
                _oloX.trace("milestone %s -> %s", _OlIx, tostring(_IooX))
            end
            task.wait(0.15)
        end
        _xOOo._ooOO = _xOOo._ooOO + _IIxl
        return _IIxl, _IIxl > 0 and ("Claimed " .. _IIxl) or "Nothing to claim yet"
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        if not _IoIx then
            _olxl = false
            _lXx = false
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            _IIlX, _loXO = nil, 0
            _XlXO, _lxX = 0, false
            _oloX._XIxo("off (%d snapshot reads this session)", _xOOo.asks)
            fireChange()
            return true
        end
        _lIlx = _XIxX.scope("features.boss")
        _olxl = true
        _XIxX.try("boss.watchState", function()
            local _oxIx = _OooX.find("RE/BossEvent/StateShifted")
            if not _oxIx then
                _oloX.warn("RE/BossEvent/StateShifted not found - running on the backstop")
                return
            end
            _lIlx:connect(_oxIx.OnClientEvent, function()
                _xOOo.stateEvents = _xOOo.stateEvents + 1
                task.spawn(function()
                    _XIxX.try("boss.stateShifted", function()
                        local _lxXX = _IIlX and _IIlX.Open
                        _xolx.snapshot(true)
                        local _IOoO = _IIlX and _IIlX.Open
                        _oloX._XIxo("state shifted: open %s -> %s",
                            tostring(_lxXX), tostring(_IOoO))
                        fireChange()
                        if _lXx and _IOoO == true and _lxXX ~= true then
                            task.wait(_oolx.ENTER_GAP)
                            local _xOIx, _oxXX = _xolx.enter()
                            if _xOIx then _xOOo.autoEntered = _xOOo.autoEntered + 1 end
                            _oloX._XIxo("auto enter on open -> %s %s",
                                tostring(_xOIx), tostring(_oxXX))
                        end
                    end)
                end)
            end)
        end)
        _lIlx:loop("backstop", _OOOX._oIOo(_oolx.BACKSTOP), function()
            local _xXOX, _lxXX = _IIlX ~= nil, _IIlX and _IIlX.Open
            readOrRetry()
            if not _xXOX or (_IIlX and _IIlX.Open) ~= _lxXX then fireChange() end
        end)
        _oloX._XIxo("on (StateShifted event + %.0fs backstop)", _OOOX._oIOo(_oolx.BACKSTOP))
        return true
    end
    return _xolx
end)
_XIxX.module("features.rift", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _OOOX  = _XIxX.require("core.device")
    local _XIXo = _XIxX.require("core.data")
    local _OooX  = _XIxX.require("core.net")
    local _OOXo = _XIxX.require("features.eggs")
    local _oloX  = _XIxX.require("boot.log").for_module("rift")
    local _xolx = {}
    local _oolx = {
        BACKSTOP    = 30,
        SNAP_TTL    = 5,
        STALE_MAX   = 8,
        DEBOUNCE    = 0.35,
        RETRY       = { 5, 10, 20 },
        NONE_LABEL  = "No pets spawned",
    }
    _xolx._oolx = _oolx
    local _lIlx        = nil
    local _olxl   = false
    local _IIlX, _loXO, _oIXl = nil, 0, 0
    local _XlXO, _lxX = 0, false
    local _lIol  = nil      -- wanted ids currently on the field
    local _IIll, _lIll = nil, nil
    local _OlIX      = nil      -- the user's chosen pet id, or nil for "any"
    local _OoIl = {}
    local _XlIo     = false
    local _xOOo = {
        askState = 0, askFailed = 0, repaints = 0, coalesced = 0,
        rotations = 0, pickCleared = 0,
    }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    local _xXIl = {}
    function _xolx.onChange(_xxxX) _xXIl[#_xXIl + 1] = _xxxX end
    local function fireChange()
        _xOOo.repaints = _xOOo.repaints + 1
        for _OXlx, _xxxX in ipairs(_xXIl) do
            task.spawn(function() _XIxX.try("rift.onChange", _xxxX) end)
        end
    end
    function _xolx.petName(_OlIx)
        local _oOOX = _XIXo.assetsDir()
        local _XlOX = _oOOX and _oOOX[_OlIx]
        return (_XlOX and _XlOX.DisplayName and tostring(_XlOX.DisplayName)) or tostring(_OlIx)
    end
    local function petNames(_lIoX)
        local _lxoX = {}
        for _OXlx, _OlIx in ipairs(_lIoX or {}) do _lxoX[#_lxoX + 1] = _xolx.petName(_OlIx) end
        return _lxoX
    end
    function _xolx._XOOo(_loIo)
        if not _olxl then return nil end
        local _XooX = _loIx.clock()
        if not _loIo and _IIlX and (_XooX - _loXO) < _oolx.SNAP_TTL then
            return _IIlX
        end
        _xOOo.askState = _xOOo.askState + 1
        local _xIlx = _OooX.call("RF/Rift/AskState")
        _loXO = _XooX
        if type(_xIlx) == "table" then
            _IIlX, _oIXl = _xIlx, _XooX
            return _IIlX
        end
        _xOOo.askFailed = _xOOo.askFailed + 1
        if (_XooX - _oIXl) > _oolx.STALE_MAX then
            _IIlX = nil
        end
        return _IIlX
    end
    function _xolx.requirements()
        local _xIlx = _xolx._XOOo()
        local _IXIX = _xIlx and _xIlx.Requirements
        if type(_IXIX) ~= "table" then return {} end
        return _IXIX
    end
    local function computeOwned()
        local _IXIX = _xolx.requirements()
        if #_IXIX == 0 then
            _IIll, _lIll = nil, nil
            return
        end
        local _IXOO = nil
        _XIxX.try("rift.readInventory", function()
            local _XOoX = _XIXo._lxIX()
            if type(_XOoX) ~= "table" or type(_XOoX.Get) ~= "function" then return end
            local _XXIO = _XOoX.Get(_OoXX.LocalPlayer)
            local _XIoX = _XXIO and _XXIO.Inventory
            if type(_XIoX) ~= "table" then return end
            _IXOO = {}
            for _OXlx, _olXX in pairs(_XIoX) do
                local _olOX = type(_olXX) == "table" and _olXX.Category or nil
                if _olOX then _IXOO[_olOX] = (_IXOO[_olOX] or 0) + 1 end
            end
        end)
        if not _IXOO then
            _IIll, _lIll = nil, nil
            return
        end
        local _xXXo, _OlIO = 0, {}
        for _OXlx, _OlIx in ipairs(_IXIX) do
            if (_IXOO[_OlIx] or 0) > 0 then
                _xXXo = _xXXo + 1
            else
                _OlIO[#_OlIO + 1] = _OlIx
            end
        end
        _IIll, _lIll = _xXXo, _OlIO
    end
    function _xolx._oolo()
        if _IIll == nil and _lIll == nil then computeOwned() end
        return _IIll, _lIll
    end
    local function computeField()
        local _IXIX = _xolx.requirements()
        if #_IXIX == 0 then
            _lIol = nil
            return
        end
        local _oolX = {}
        for _OXlx, _OlIx in ipairs(_IXIX) do _oolX[_OlIx] = true end
        local _OOxo = _OOXo._OOxo()
        if not _OOxo then
            _lIol = nil
            return
        end
        local _oxIX, _lxoX = {}, {}
        for _OXlx, _lxlx in ipairs(_OOxo) do
            local _olOX = _lxlx.assetCategory
            if _olOX and _oolX[_olOX] and not _oxIX[_olOX] then
                _oxIX[_olOX] = true
                _lxoX[#_lxoX + 1] = _olOX
            end
        end
        _lIol = _lxoX
    end
    function _xolx.onField()
        if not _olxl then return {} end
        if not _lIol then computeField() end
        return _lIol or {}
    end
    function _xolx.petIsOut(_OlIx)
        if not _OlIx then return false end
        for _OXlx, _lxoX in ipairs(_xolx.onField()) do
            if _lxoX == _OlIx then return true end
        end
        return false
    end
    function _xolx._OOIO()
        local _lxoX = {}
        _OoIl = {}
        for _OXlx, _OlIx in ipairs(_lIol or {}) do
            local _xxIo = _xolx.petName(_OlIx)
            _OoIl[_xxIo] = _OlIx
            _lxoX[#_lxoX + 1] = _xxIo
        end
        if #_lxoX == 0 then _lxoX[1] = _oolx.NONE_LABEL end
        return _lxoX
    end
    function _xolx.idForLabel(_xxIo)
        if type(_xxIo) ~= "string" or _xxIo == _oolx.NONE_LABEL then return nil end
        return _OoIl[_xxIo] or _xxIo
    end
    function _xolx._OlIX() return _OlIX end
    function _xolx.setPick(_OlIx)
        _OlIX = _OlIx
        if _OlIx then
            _oloX._XIxo("targeting %s", _xolx.petName(_OlIx))
        else
            _oloX._XIxo("targeting any required rift pet")
        end
    end
    local function prunePick()
        if not _OlIX then return false end
        if _xolx.petIsOut(_OlIX) then return false end
        _xOOo.pickCleared = _xOOo.pickCleared + 1
        _oloX._XIxo("%s is no longer out - clearing the pick", _xolx.petName(_OlIX))
        _OlIX = nil
        return true
    end
    function _xolx._IXXO()
        if not _olxl then return { _OXOo = "Rift", _Ixoo = "off" } end
        local _xIlx = _IIlX
        if not _xIlx then
            return { _OXOo = "Rift", _Ixoo = (_xOOo.askState > 0)
                and "Unavailable  \u{B7}  retrying"
                or "Reading..." }
        end
        if _xIlx.Unlocked == false then
            local _xXxo = tonumber(_xIlx.UnlockSpeedPower)
            return {
                _OXOo = "Rift",
                _Ixoo = _xXxo
                    and ("Unlocks at " .. _OOXo.formatRate(_xXxo) .. " speed")
                    or "Locked",
            }
        end
        local _IXIX = _xIlx.Requirements or {}
        local _xXXo, _OlIO = _IIll, _lIll
        local _llOO = tostring(_xIlx.BannerDisplayName or _xIlx.BannerId or "Rift")
        local _OxIX = (tonumber(_xIlx.SecondsUntilRotation) or 0) - (_loIx.clock() - _oIXl)
        local _ooxo = math._IOoX(0, math.floor(_OxIX / 60))
        local _OXOo = _xXXo and ("%s  %d/%d"):format(_llOO, _xXXo, #_IXIX) or _llOO
        local _lxOO = {}
        local _XlIX, _xoIO = tonumber(_xIlx.PityCount), tonumber(_xIlx.PityThreshold)
        if _XlIX and _xoIO then
            _lxOO[#_lxOO + 1] = ("pity %d/%d"):format(_XlIX, _xoIO)
        end
        local _OoXo = tonumber(_xIlx.FreeRefreshesRemaining)
        if _OoXo then _lxOO[#_lxOO + 1] = ("%d free"):format(_OoXo) end
        local _lllX = ("%dm"):format(_ooxo)
        if #_lxOO > 0 then _lllX = _lllX .. "  \u{B7}  " .. table.concat(_lxOO, "  \u{B7}  ") end
        if _xXXo and #_IXIX > 0 and _xXXo >= #_IXIX then
            return { _OXOo = _OXOo, _Ixoo = ("All pets ready  \u{B7}  new rift in %s"):format(_lllX) }
        end
        local _oolX = (_OlIO and #_OlIO > 0) and _OlIO or _IXIX
        if #_oolX == 0 then
            return { _OXOo = _OXOo, _Ixoo = ("New rift in %s"):format(_lllX) }
        end
        local _XXoO = {}
        for _OXlx, _OlIx in ipairs(_lIol or {}) do _XXoO[_OlIx] = true end
        local _Xxlo = {}
        for _OXlx, _OlIx in ipairs(_oolX) do
            if _XXoO[_OlIx] then _Xxlo[#_Xxlo + 1] = _xolx.petName(_OlIx) end
        end
        local _Ixoo
        if #_Xxlo > 0 then
            _Ixoo = ("Steal %s now"):format(table.concat(_Xxlo, ", "))
        elseif #_oolX == 1 then
            _Ixoo = ("Need %s  \u{B7}  not spawned"):format(_xolx.petName(_oolX[1]))
        else
            _Ixoo = ("Need %d: %s  \u{B7}  none spawned")
                :format(#_oolX, table.concat(petNames(_oolX), ", "))
        end
        return { _OXOo = _OXOo, _Ixoo = ("%s  \u{B7}  %s"):format(_Ixoo, _lllX) }
    end
    function _xolx.eligible()
        if not _olxl then return false end
        local _xXXo, _OlIO = _xolx._oolo()
        if _xXXo and #_xolx.requirements() > 0 and _xXXo >= #_xolx.requirements() then
            return false
        end
        local _xXxo = {}
        for _OXlx, _OlIx in ipairs((_OlIO and #_OlIO > 0) and _OlIO or _xolx.requirements()) do
            _xXxo[_OlIx] = true
        end
        if _OlIX then return _xolx.petIsOut(_OlIX) and _xXxo[_OlIX] ~= nil end
        for _OXlx, _OlIx in ipairs(_xolx.onField()) do
            if _xXxo[_OlIx] then return true end
        end
        return false
    end
    function _xolx.pickTarget()
        if not _olxl then return nil, "rift is off" end
        local _xXXo, _OlIO = _xolx._oolo()
        local _IXIX = _xolx.requirements()
        if #_IXIX == 0 then return nil, "rift has no requirements" end
        if _xXXo and _xXXo >= #_IXIX then return nil, "all rift pets owned" end
        local _xXxo = {}
        for _OXlx, _OlIx in ipairs((_OlIO and #_OlIO > 0) and _OlIO or _IXIX) do
            _xXxo[_OlIx] = true
        end
        local _OOxo = _OOXo._OOxo()
        if not _OOxo then return nil, "no egg list" end
        for _OXlx, _lxlx in ipairs(_OOxo) do
            local _olOX = _lxlx.assetCategory
            if _olOX and _xXxo[_olOX] then
                if _OlIX then
                    if _olOX == _OlIX then return _lxlx end
                else
                    return _lxlx
                end
            end
        end
        return nil, _OlIX
            and ("%s is not on the field"):format(_xolx.petName(_OlIX))
            or "no required rift pet is on the field"
    end
    local _OolO, _lolO, _oolO = nil, false, false
    local _Ioxo          -- defined below with recompute; tryTrade calls it
    function _xolx.autoTradeOn() return _lolO end
    local function riftHave(_IXIX)
        if type(_IXIX) ~= "table" or #_IXIX == 0 then return nil end
        local _lxoX, _xllo = {}, false
        for _OXlx, _IlOx in ipairs(_IXIX) do _lxoX[_IlOx] = _lxoX[_IlOx] or { _oolo = 0, _XOlX = {} } end
        _XIxX.try("rift.tradeInventory", function()
            local _XOoX = _XIXo._lxIX()
            local _XOIX = type(_XOoX) == "table" and _XOoX.Get and _XOoX.Get(_OoXX.LocalPlayer)
            local _XIoX = _XOIX and _XOIX.Inventory
            if type(_XIoX) ~= "table" then return end
            _xllo = true
            local _XOo, _oOo
            pcall(function() _XOo = require(_OoXX.ReplicatedStorage.Shared.Util._XOo) end)
            pcall(function() _oOo = require(_OoXX.ReplicatedStorage.Shared.Util._oOo) end)
            local _XXOl = {}
            for _OXlx, _olOx in pairs(_XOIX.EquippedAssets or {}) do _XXOl[_olOx] = true end
            local _lIxO = {}
            for _OXXX, _olXX in pairs(_XIoX) do
                local _olOX = type(_olXX) == "table" and (_olXX.Category or (_olXX.ItemData and _olXX.ItemData.Category))
                local _xxIX = _olOX and _lxoX[_olOX]
                if _xxIX then
                    _xxIX._oolo = _xxIX._oolo + 1
                    local _lOoX = not _XXOl[_OXXX]
                    if _lOoX and _XOo and _XOo.MayEnterRift then
                        local _xOIx, _IlOx = pcall(_XOo.MayEnterRift, _OXXX, _olXX)
                        _lOoX = _xOIx and _IlOx == true
                    end
                    if _lOoX then
                        local _xlOx = math.huge
                        if _oOo then
                            pcall(function() _xlOx = _oOo.WeightKg(_oOo.Decode(_olXX)) end)
                        end
                        _lIxO[_OXXX] = _xlOx
                        _xxIX._XOlX[#_xxIX._XOlX + 1] = _OXXX
                    end
                end
            end
            for _OXlx, _xxIX in pairs(_lxoX) do
                table._lIlX(_xxIX._XOlX, function(_oXlx, _XXlx) return (_lIxO[_oXlx] or 0) < (_lIxO[_XXlx] or 0) end)
            end
        end)
        return _xllo and _lxoX or nil
    end
    local function tryTrade()
        if _oolO then return nil end
        _oolO = true
        local _olXO = nil
        _XIxX.try("rift.tryTrade", function()
            local _xIlx = _xolx._XOOo(true)
            if type(_xIlx) ~= "table" then return end
            if _xIlx.PendingReward then
                _OooX.call("RF/Rift/AskFinishReveal")
                _olXO = "revealed"
                return
            end
            local _IXIX = _xIlx.Requirements
            if type(_IXIX) ~= "table" or #_IXIX < 3 then return end
            local _xXXo = riftHave(_IXIX)
            if not _xXXo then return end
            local _XOlX, _IolX = {}, {}
            for _xxlx = 1, 3 do
                local _xxIX = _xXXo[_IXIX[_xxlx]]
                for _OXlx, _olOx in ipairs(_xxIX and _xxIX._XOlX or {}) do
                    if not _IolX[_olOx] then _XOlX[_xxlx] = _olOx _IolX[_olOx] = true break end
                end
                if not _XOlX[_xxlx] then return end      -- not ready yet
            end
            local _OlXX, _IooX = _OooX.call("RF/Rift/AskTradeIn", _XOlX)
            if _OlXX ~= true then
                _olXO = "refused: " .. tostring(_IooX or _OlXX)
                return
            end
            task.wait(1)
            _OooX.call("RF/Rift/AskFinishReveal")
            _olXO = "traded"
        end)
        _oolO = false
        if _olXO then
            _IIll, _lIll = nil, nil
            _Ioxo("traded")
        end
        return _olXO
    end
    local _XX = {}
    function _xolx.onTrade(_xxxX) _XX[#_XX + 1] = _xxxX end
    function _xolx.setAutoTrade(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _lolO then return true end
        _lolO = _IoIx
        if not _IoIx then
            if _OolO then _OolO:destroy() _OolO = nil end
            _oloX._XIxo("auto trade-in OFF")
            return true
        end
        if not _olxl then _xolx.setEnabled(true) end
        _OolO = _XIxX.scope("features.rift.trade")
        _OolO:loop("trade", _OOOX._oIOo(5), function()
            local _IlOx = tryTrade()
            if _IlOx == "traded" then
                _oloX._XIxo("traded the 3 pets in - Rift Egg claimed")
            elseif _IlOx == "revealed" then
                _oloX._XIxo("finished a pending reveal")
            elseif _IlOx then
                _oloX.warn("trade-in %s", tostring(_IlOx))
            end
            if _IlOx then
                for _OXlx, _xxxX in ipairs(_XX) do
                    task.spawn(function() _XIxX.try("rift.onTrade", _xxxX, _IlOx) end)
                end
            end
        end)
        _oloX._XIxo("auto trade-in ON (every 5s, lightest eligible pet of each kind, never equipped)")
        return true
    end
    local _Xll
    local function recompute(_oxXX, _XoXo)
        _XlIo = false
        if _XoXo then
            _loXO = 0            -- force the next state() to re-read
            local _xIlx = _xolx._XOOo(true)
            if _xIlx then
                _XlXO = 0
            else
                _Xll()
            end
        end
        if _XoXo or (_IIll == nil and _lIll == nil) then computeOwned() end
        computeField()
        prunePick()
        _oloX.trace("recomputed (%s)", tostring(_oxXX))
        fireChange()
    end
    _Xll = function()
        if _lxX or not _lIlx then return end
        local wait = _oolx.RETRY[_XlXO + 1]
        if not wait then return end
        _lxX = true
        _oloX.warn("rift read failed - retrying in %ds", wait)
        _lIlx:delay("retry", _OOOX._oIOo(wait), function()
            _lxX = false
            _XlXO = _XlXO + 1
            recompute("retry " .. _XlXO, true)
        end)
    end
    _xolx._oxIO = function(_oxXX)
        if not _olxl then return false end
        _OOXo.invalidate("rift refresh")
        recompute(_oxXX or "manual refresh", true)
        return true
    end
    _Ioxo = function(_oxXX)
        if _XlIo then
            _xOOo.coalesced = _xOOo.coalesced + 1
            return
        end
        _XlIo = true
        if not _lIlx then return end
        _lIlx:delay("recompute", _oolx.DEBOUNCE, function()
            if _XlIo then recompute(_oxXX, false) end
        end)
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        if not _IoIx then
            _olxl = false
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            _IIlX, _loXO, _oIXl = nil, 0, 0
            _lIol, _IIll, _lIll = nil, nil, nil
            _OoIl, _XlIo = {}, false
            _XlXO, _lxX = 0, false
            _OlIX = nil
            _oloX._XIxo("off (%d state reads, %d repaints this session)",
                _xOOo.askState, _xOOo.repaints)
            fireChange()
            return true
        end
        _lIlx = _XIxX.scope("features.rift")
        _olxl = true
        _XIxX.try("rift.watchRotation", function()
            local _oxIx = _OooX.find("RE/Rift/BannerRotated")
            if not _oxIx then
                _oloX.warn("RE/Rift/BannerRotated not found - running on the backstop")
                return
            end
            _lIlx:connect(_oxIx.OnClientEvent, function()
                _xOOo.rotations = _xOOo.rotations + 1
                _oloX._XIxo("banner rotated - re-reading")
                task.spawn(function()
                    _XIxX.try("rift.rotated", function() recompute("banner rotated", true) end)
                end)
            end)
        end)
        _XIxX.try("rift.watchField", function()
            local _xIxX = _XIXo.eggState()
            if not _xIxX then return end
            for _OXlx, _oXxo in ipairs({ "FieldRefreshed", "FieldGone", "FieldShifted" }) do
                local _lOXX = _xIxX[_oXxo]
                if _lOXX and type(_lOXX) == "table" and type(_lOXX.Connect) == "function" then
                    _lIlx:connect(_lOXX, function() _Ioxo("field " .. _oXxo) end)
                end
            end
        end)
        _XIxX.try("rift.watchSave", function()
            local _XOoX = _XIXo._lxIX()
            local _lOXX = type(_XOoX) == "table" and _XOoX.FieldChanged or nil
            if _lOXX and type(_lOXX) == "table" and type(_lOXX.Connect) == "function" then
                _lIlx:connect(_lOXX, function(_lOIo)
                    if _lOIo == nil or _lOIo == "Inventory" then
                        _IIll, _lIll = nil, nil
                        _Ioxo("inventory changed")
                    end
                end)
            end
        end)
        _lIlx:loop("backstop", _OOOX._oIOo(_oolx.BACKSTOP), function()
            recompute(_IIlX and "backstop" or "first read", true)
        end)
        _oloX._XIxo("on (rotation event + field signals, backstop %.0fs)",
            _OOOX._oIOo(_oolx.BACKSTOP))
        return true
    end
    return _xolx
end)
_XIxX.module("features.eggs", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _OOOX = _XIxX.require("core.device")
    local _XIXo = _XIxX.require("core.data")
    local _oloX = _XIxX.require("boot.log").for_module("eggs")
    local _xolx = {}
    local _oolx = {
        CACHE_TTL       = 0.5,   -- how long a built list stays good (scaled by device)
        MIN_REBUILD     = 0.1,   -- floor between rebuilds, so a signal burst costs one
        RAW_TTL         = 0.25,  -- how long a raw snapshot stays good
        FALLBACK_TTL    = 5.0,   -- the Workspace walk: rarely, and never in a loop
        STOLEN_FOR      = 120,   -- keep a stolen uid suppressed this long
        UNREACHABLE_FOR = 45,    -- V3.1 K.UNREACHABLE_COOLDOWN
        PARTIAL_FLOOR   = 8,     -- <= this many records after a full field = replication lag
        FULL_FIELD_MIN  = 10,    -- > this many records means we have seen the real field
        VALUE_CACHE_MAX = 600,   -- hard ceiling; the field is ~55, so this is generous
    }
    _xolx._oolx = _oolx
    local _lxll, _Ix, _Olx
    _XIxX.try("eggs.resolveModules", function()
        _lxll = _XIXo.eggState()
        _Ix = _XIXo.assetEarnings()
        _Olx = _XIXo.assetsDir()
    end)
    _xolx._Xxlo = (_lxll ~= nil)
    if not _xolx._Xxlo then
        _oloX.error("EggState not found - is this Steal An Egg?")
    end
    local _IxIO, _llll = nil, 0
    local _XlIo, _ooO = false, nil
    local _OOxo, _xOoO       = nil, 0
    local _XIX         = 0
    local _IIO       = false
    local _llo        = false
    local _lXXO             = {}   -- uid -> os.clock() when we took it
    local _lOo        = {}   -- uid -> os.clock() when it beat us
    local _llx         = {}   -- uid -> income/sec
    local _OOo        = 0
    local _xOOo = {
        scans = 0, cacheHits = 0, partialHeld = 0, fallbacks = 0,
        signals = 0, dirtyRebuilds = 0,
        lastScanMs = 0, lastConsidered = 0, lastKept = 0,
    }
    _XIxX._XXIO._lIoo("eggs.list", function() return _OOxo and #_OOxo or 0 end)
    _XIxX._XXIO._lIoo("eggs.values", function() return _OOo end)
    _XIxX._XXIO._lIoo("eggs.unreachable", function()
        local _oIOx = 0
        for _OXlx in pairs(_lOo) do _oIOx = _oIOx + 1 end
        return _oIOx
    end)
    _XIxX._XXIO._lIoo("eggs.stolen", function()
        local _oIOx = 0
        for _OXlx in pairs(_lXXO) do _oIOx = _oIOx + 1 end
        return _oIOx
    end)
    function _xolx.invalidate(_XIXO)
        _OOxo, _xOoO = nil, 0
        _IxIO, _llll = nil, 0
        _XlIo = false
        if _XIXO then _oloX.trace("invalidated: %s", _XIXO) end
    end
    function _xolx.markDirty(_XIXO)
        _XlIo = true
        _ooO = _XIXO
        _xOOo.signals = (_xOOo.signals or 0) + 1
    end
    function _xolx.markStolen(_OXXX)
        if _OXXX then _lXXO[tostring(_OXXX)] = _loIx.clock() end
    end
    function _xolx.markUnreachable(_OXXX)
        if _OXXX then _lOo[tostring(_OXXX)] = _loIx.clock() end
    end
    function _xolx.clearUnreachable(_OXXX)
        if _OXXX then _lOo[tostring(_OXXX)] = nil end
    end
    local function pruneStolen()
        local _XooX = _loIx.clock()
        for _OXXX, _oOxX in pairs(_lXXO) do
            if (_XooX - _oOxX) > _oolx.STOLEN_FOR then _lXXO[_OXXX] = nil end
        end
        for _OXXX, _oOxX in pairs(_lOo) do
            if (_XooX - _oOxX) > _oolx.UNREACHABLE_FOR then _lOo[_OXXX] = nil end
        end
    end
    local function calcValue(_XIXX)
        local _OXXX = _XIXX.Uid
        local _lxOX = _llx[_OXXX]
        if _lxOX then return _lxOX end
        local _Ilxo = {
            Category  = _XIXX.AssetCategory,
            Scale     = tonumber(_XIXX.AssetScale) or 1,
            Mutations = _XIXX.Mutations or {},
        }
        local _XlOx = 0
        if _Ix then
            local _xOIx, _ooIX = pcall(_Ix.LiveRatePerSecond, _Ilxo, nil, nil, _OoXX.LocalPlayer)
            if _xOIx and type(_ooIX) == "number" then
                _XlOx = _ooIX
            else
                _xOIx, _ooIX = pcall(_Ix.MutationOnlyRatePerSecond, _Ilxo)
                if _xOIx and type(_ooIX) == "number" then _XlOx = _ooIX end
            end
        end
        if _OOo >= _oolx.VALUE_CACHE_MAX then
            _oloX.warn("value cache hit %d entries - clearing", _OOo)
            _llx, _OOo = {}, 0
        end
        _llx[_OXXX] = _XlOx
        _OOo = _OOo + 1
        return _XlOx
    end
    _xolx._XxOo = calcValue
    local function displayName(_XIXX)
        local _oOOX = _Olx and _Olx[_XIXX.AssetCategory]
        return (_oOOX and _oOOX.DisplayName) or _XIXX.AssetCategory
            or ("Egg " .. tostring(_XIXX.Uid or "?"):_loXX(1, 6))
    end
    local function rarityIdOf(_XIXX)
        local _oOOX = _Olx and _Olx[_XIXX.AssetCategory]
        if _oOOX and _oOOX.Rarity then
            return _oOOX.Rarity._id or _oOOX.Rarity.DisplayName or "?"
        end
        return "?"
    end
    local function rarityOf(_XIXX)
        local _oOOX = _Olx and _Olx[_XIXX.AssetCategory]
        if _oOOX and _oOOX.Rarity then
            return _oOOX.Rarity.DisplayName or _oOOX.Rarity._id or "?"
        end
        return "?"
    end
    local function weightOf(_XIXX)
        local _oOOX = _Olx and _Olx[_XIXX.AssetCategory]
        local _lXoo = _oOOX and _oOOX.Egg and tonumber(_oOOX.Egg.WeightKg)
        if not _lXoo then return 0 end
        return _lXoo * (tonumber(_XIXX.AssetScale) or 1)
    end
    function _xolx.formatRate(_oIOx)
        _oIOx = tonumber(_oIOx) or 0
        for _OXlx, _olOx in ipairs({ { 1e12, "T" }, { 1e9, "B" }, { 1e6, "M" }, { 1e3, "K" } }) do
            if _oIOx >= _olOx[1] then
                local _XlOx = _oIOx / _olOx[1]
                local _lXXX = (_XlOx < 10) and string.format("%.2f", _XlOx) or string.format("%.1f", _XlOx)
                return (_lXXX:gsub("%.?0+$", "")) .. _olOx[2]
            end
        end
        return tostring(math.floor(_oIOx))
    end
    local function readField()
        local _OxIO = nil
        _XIxX.try("eggs.readField", function()
            local _XIXo = _lxll and _lxll.ReadFieldEggs and _lxll.ReadFieldEggs()
            if type(_XIXo) == "table" and type(_XIXo.Records) == "table" then
                _OxIO = _XIXo.Records
            end
        end)
        return _OxIO
    end
    local function readFallback()
        local _XooX = _loIx.clock()
        if (_XooX - _XIX) < _oolx.FALLBACK_TTL then return nil end
        _XIX = _XooX
        _xOOo.fallbacks = _xOOo.fallbacks + 1
        local _OxIO = {}
        _XIxX.try("eggs.fallback", function()
            local _OlOo = workspace:FindFirstChild("AreaEggSlotsClient")
            if not _OlOo then return end
            for _OXlx, _OIOx in ipairs(_OlOo:GetChildren()) do
                if _OIOx:IsA("Model") then
                    local _OXXX = _OIOx:GetAttribute("Uid") or _OIOx:GetAttribute("EggUid") or _OIOx.Name
                    local _IXxX
                    local _lxOX = _OIOx:FindFirstChild("Hitbox")
                    if _lxOX and _lxOX:IsA("BasePart") then _IXxX = _lxOX.CFrame else _IXxX = _OIOx:GetPivot() end
                    if _OXXX and _IXxX then
                        _OxIO[#_OxIO + 1] = {
                            Uid = tostring(_OXXX), BoundsCFrame = _IXxX, State = "Slot",
                        }
                    end
                end
            end
        end)
        _oloX._XIxo("fallback scan: %d records from AreaEggSlotsClient (no EggState - names and values unavailable)", #_OxIO)
        return #_OxIO > 0 and _OxIO or nil
    end
    local function snapshot(_loIo)
        local _XooX = _loIx.clock()
        if not _loIo and _IxIO and (_XooX - _llll) < _OOOX._oIOo(_oolx.RAW_TTL) then
            return _IxIO
        end
        local _OxIO = readField()
        if not _OxIO or #_OxIO == 0 then
            _OxIO = readFallback() or _OxIO
        end
        if _OxIO then
            _IxIO, _llll = _OxIO, _XooX
        end
        return _IxIO
    end
    function _xolx._OOxo(_Xxxo, _loIo)
        _Xxxo = _Xxxo or {}
        local _XooX = _loIx.clock()
        local _XoIo = (_XooX - _xOoO) < _OOOX._oIOo(_oolx.CACHE_TTL)
        local _XOX = (_XooX - _xOoO) >= _oolx.MIN_REBUILD
        if not _loIo and _OOxo and _XoIo and not (_XlIo and _XOX) then
            _xOOo.cacheHits = _xOOo.cacheHits + 1
            return _OOxo
        end
        if _XlIo and _XOX then
            _xOOo.dirtyRebuilds = (_xOOo.dirtyRebuilds or 0) + 1
            _XlIo = false
        end
        local _Ollx = _loIx.clock()
        local _OxIO = snapshot(_loIo)
        local _oIOx = _OxIO and #_OxIO or 0
        if _oIOx > _oolx.FULL_FIELD_MIN then _IIO = true end
        if _IIO and _oIOx > 0 and _oIOx <= _oolx.PARTIAL_FLOOR and _OOxo and #_OOxo > 0 then
            if not _llo then
                _llo = true
                _xOOo.partialHeld = _xOOo.partialHeld + 1
                _oloX._XIxo("only %d records replicated - field still loading, keeping the last %d",
                    _oIOx, #_OOxo)
            end
            return _OOxo
        end
        _llo = false
        if not _OxIO then
            _OOxo = _OOxo or {}
            _xOoO = _XooX
            return _OOxo
        end
        pruneStolen()
        local _xIOl = _Xxxo._XOOo or { Slot = true, Dropped = true }
        local _lxoX, _oxIX = {}, {}
        local _xxo, _xlIo = 0, 0
        for _OXlx, _XIXX in ipairs(_OxIO) do
            _xxo = _xxo + 1
            local _OXXX = _XIXX.Uid and tostring(_XIXX.Uid)
            if _OXXX and not _oxIX[_OXXX] then
                _oxIX[_OXXX] = true
                if not _xIOl[_XIXX.State] then
                elseif _lXXO[_OXXX] then
                elseif _lOo[_OXXX] then
                else
                    local _XxOo = calcValue(_XIXX)
                    local _IIXX = _XIXX.BoundsCFrame and _XIXX.BoundsCFrame.Position
                    if _IIXX and (not _Xxxo.minValue or _XxOo >= _Xxxo.minValue)
                       and (not _Xxxo._xxOO or _Xxxo._xxOO(_XIXX, _XxOo)) then
                        _lxoX[#_lxoX + 1] = {
                            _OXXX   = _OXXX,
                            _XOOo = _XIXX.State,
                            _IIXX   = _IIXX,          -- Vector3, not an Instance
                            _XxOo = _XxOo,
                            _oXxo  = displayName(_XIXX),
                            _lIXO = rarityOf(_XIXX),
                            rarityId = rarityIdOf(_XIXX),
                            assetCategory = _XIXX.AssetCategory,
                            _OIxo = (function()
                                local _Ixlx = _Olx and _XIXX.AssetCategory and _Olx[_XIXX.AssetCategory]
                                local _xxlx = _Ixlx and _Ixlx.Icon
                                if type(_xxlx) == "number" then return "rbxassetid://" .. tostring(_xxlx) end
                                if type(_xxlx) == "string" and _xxlx ~= "" then
                                    return _xxlx:match("^%d+$") and ("rbxassetid://" .. _xxlx) or _xxlx
                                end
                                return nil
                            end)(),
                            assetScale = _XIXX.AssetScale,
                            mutations = _XIXX.Mutations,
                            _XlIx    = weightOf(_XIXX),
                            guardHeld = (_XIXX.State == "GuardCarried"),
                            _llxl   = (_XIXX.State == "Dropped"),
                            _oIOO = _XIXX.AreaId,
                            _IXoO = _XIXX.NestId,
                        }
                    end
                end
            elseif _OXXX then
                _xlIo = _xlIo + 1
            end
        end
        table._lIlX(_lxoX, function(_oXlx, _XXlx) return _oXlx._XxOo > _XXlx._XxOo end)
        if _OOo > (#_lxoX * 2 + 50) then
            local _llxo, _Olxo = {}, 0
            for _OXlx, _lxlx in ipairs(_lxoX) do
                local _XlOx = _llx[_lxlx._OXXX]
                if _XlOx ~= nil then
                    _llxo[_lxlx._OXXX] = _XlOx
                    _Olxo = _Olxo + 1
                end
            end
            _oloX.trace("value cache pruned %d -> %d (field %d)", _OOo, _Olxo, #_lxoX)
            _llx, _OOo = _llxo, _Olxo
        end
        _OOxo, _xOoO = _lxoX, _XooX
        _xOOo.scans = _xOOo.scans + 1
        _xOOo.lastScanMs = (_loIx.clock() - _Ollx) * 1000
        _xOOo.lastConsidered = _xxo
        _xOOo.lastKept = #_lxoX
        _oloX.trace("scan: %d records -> %d takeable (%d dupes) in %.1fms, best %s %s/s",
            _xxo, #_lxoX, _xlIo, _xOOo.lastScanMs,
            _lxoX[1] and _lxoX[1]._oXxo or "-",
            _lxoX[1] and string.format("%.0f", _lxoX[1]._XxOo) or "-")
        return _OOxo
    end
    function _xolx._oXoo(_Xxxo)
        local _lIOx = _xolx._OOxo(_Xxxo)
        return _lIOx and _lIOx[1] or nil
    end
    function _xolx.get(_OXXX)
        if not _OXXX then return nil end
        local _XIXX
        _XIxX.try("eggs.get", function()
            _XIXX = _lxll and _lxll.ReadFieldEgg and _lxll.ReadFieldEgg(_OXXX)
        end)
        if not _XIXX then return nil end
        return {
            _OXXX   = tostring(_OXXX),
            _XOOo = _XIXX.State,
            _IIXX   = _XIXX.BoundsCFrame and _XIXX.BoundsCFrame.Position,
            _XxOo = calcValue(_XIXX),
            _oXxo  = displayName(_XIXX),
            _lIXO = rarityOf(_XIXX),
            rarityId = rarityIdOf(_XIXX),
            assetCategory = _XIXX.AssetCategory,
            assetScale = _XIXX.AssetScale,
            mutations = _XIXX.Mutations,
            _XlIx    = weightOf(_XIXX),
            _oIOO = _XIXX.AreaId,
            _IXoO = _XIXX.NestId,
        }
    end
    function _xolx.carryingUid()
        local _OoIo
        local _OOIx = _OoXX.Players.LocalPlayer and _OoXX.Players.LocalPlayer.UserId
        _XIxX.try("eggs.carryingUid", function()
            local _XIXo = _lxll and _lxll.ReadFieldEggs and _lxll.ReadFieldEggs()
            for _OXlx, _IlOx in pairs(_XIXo and _XIXo.Records or {}) do
                if _IlOx.State == "Carried"
                    and (_IlOx.CarrierUserId == nil or tonumber(_IlOx.CarrierUserId) == _OOIx) then
                    _OoIo = tostring(_IlOx.Uid)
                    break
                end
            end
        end)
        return _OoIo
    end
    function _xolx.stillTakeable(_OXXX, _xoXO)
        local _IlOx = _xolx.get(_OXXX)
        if not _IlOx then return false, "gone" end
        local _xOIx = (_xoXO or { Slot = true, Dropped = true })[_IlOx._XOOo]
        return _xOIx and true or false, _IlOx._XOOo
    end
    function _xolx._xOOo()
        local _llOx = table._OIIo(_xOOo)
        _llOx.listSize = _OOxo and #_OOxo or 0
        _llOx._llx = _OOo
        _llOx._IIO = _IIO
        return _llOx
    end
    local _lOxO = {
        "CarryChanged",      -- an egg changed hands
        "FieldShifted",      -- the field moved
        "FieldRefreshed",    -- bulk refresh
        "FieldGone",         -- an egg left the field
        "FieldClaimed",      -- someone claimed one
        "SnapshotRefreshed", -- the underlying snapshot re-synced
    }
    local _lIlx = _XIxX.scope("features.eggs")
    local _OXlO = 0
    if _lxll then
        for _OXlx, _oXxo in ipairs(_lOxO) do
            _XIxX.try("eggs.watch." .. _oXxo, function()
                local _lOXX = _lxll[_oXxo]
                if _lOXX and type(_lOXX) == "table" and type(_lOXX.Connect) == "function" then
                    _lIlx:connect(_lOXX, function() _xolx.markDirty(_oXxo) end)
                    _OXlO = _OXlO + 1
                end
            end)
        end
    end
    _oloX._XIxo("watching %d/%d EggState signals", _OXlO, #_lOxO)
    _XIxX.require("core.character").onSpawn(_lIlx, "eggs.respawn", function()
        _xolx.invalidate("respawn")
    end)
    return _xolx
end)
_XIxX.module("features.grab", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _XIXo = _XIxX.require("core.data")
    local _oOXo = _XIxX.require("core.exec")
    local _lXxX   = _XIxX.require("core.character")
    local _OOOX  = _XIxX.require("core.device")
    local _OOXo = _XIxX.require("features.eggs")
    local _oloX  = _XIxX.require("boot.log").for_module("grab")
    local RunService = _OoXX.RunService
    local _xolx = {}
    local _oolx = {
        PROMPT_CACHE   = 30,    -- how long the prompt list stays good; they do not move
        PROMPT_NEAR    = 14,    -- a prompt this close to the egg belongs to it
        PROMPT_WAIT    = 0.6,   -- wait for the game to hand a prompt over
        STEP_INSIDE    = 3,     -- studs inside MaxActivationDistance to stand
        CONFIRM_WINDOW = 1.2,   -- how long to wait for a witness after firing
        TRIES          = 3,
        RETRY_GAP      = 0.15,  -- never zero: a retry without a yield is a spin
        TP_PROMPT_WAIT = 1.2,   -- after a teleport, how long to wait for a prompt
    }
    _xolx._oolx = _oolx
    local _lxll = _XIXo.eggState()
    local _xXIO, _xIll = nil, 0
    _XIxX._XXIO._lIoo("grab.prompts", function() return _xXIO and #_xXIO or 0 end)
    local function promptList()
        local _XooX = _loIx.clock()
        if _xXIO and (_XooX - _xIll) < _oolx.PROMPT_CACHE then
            return _xXIO
        end
        local _Ollx = _loIx.clock()
        local _OoIo = {}
        for _OXlx, _Ixlx in ipairs(workspace:GetDescendants()) do
            if _Ixlx:IsA("ProximityPrompt") then
                local _lXXX = string.lower(tostring(_Ixlx.ActionText) .. " "
                    .. tostring(_Ixlx.ObjectText) .. " " .. _Ixlx.Name)
                if _lXXX:find("steal") or _lXXX:find("carry") then
                    _OoIo[#_OoIo + 1] = _Ixlx
                end
            end
        end
        _xXIO, _xIll = _OoIo, _XooX
        _oloX.trace("prompt cache rebuilt: %d prompts in %.1fms", #_OoIo, (_loIx.clock() - _Ollx) * 1000)
        return _xXIO
    end
    local function promptPos(_xIOx)
        local _xXoO = _xIOx.Parent
        if not _xXoO then return nil end
        if _xXoO:IsA("BasePart") then return _xXoO.Position end
        if _xXoO:IsA("Model") then return _xXoO:GetPivot().Position end
        return nil
    end
    function _xolx.waitForPrompt(_xoll, _IoOO, _xIlO)
        if typeof(_xoll) ~= "Vector3" then return false end
        local _IooO = promptList()
        local _Ollx = _loIx.clock()
        local _oxXO = _Ollx + _OOOX._oIOo(_xIlO or _oolx.TP_PROMPT_WAIT)
        repeat
            if _IoOO and _IoOO() then return false end
            for _OXlx, _Ixlx in ipairs(_IooO) do
                if _Ixlx.Parent and _Ixlx.Enabled then
                    local _IIXX = promptPos(_Ixlx)
                    if _IIXX and (_IIXX - _xoll).Magnitude <= _oolx.PROMPT_NEAR then
                        _oloX.trace("prompt arrived after %.2fs", _loIx.clock() - _Ollx)
                        return true
                    end
                end
            end
            task.wait(0.05)
        until _loIx.clock() > _oxXO
        _oloX.trace("prompt never showed after %.2fs", _loIx.clock() - _Ollx)
        return false
    end
    function _xolx.confirm(_OXXX, baseWalkSpeed, _IoO)
        if _IoO then return true, "CarryChanged" end
        local _IIoX = _lXxX.humanoid()
        if _IIoX and baseWalkSpeed and _IIoX.WalkSpeed and _IIoX.WalkSpeed < (baseWalkSpeed - 1) then
            return true, "walkspeed drop"
        end
        local _xxoo = _lXxX.get()
        if _xxoo then
            for _OXlx, _xXlx in ipairs(_xxoo:GetChildren()) do
                if _xXlx:IsA("Tool") and _xXlx:GetAttribute("ItemType") == "AssetEgg"
                   and tostring(_xXlx:GetAttribute("UID")) == tostring(_OXXX) then
                    return true, "egg tool in hand"
                end
            end
        end
        local _XIXX = _OOXo.get(_OXXX)
        if _XIXX and _XIXX._XOOo == "Carried" then return true, "ReadFieldEgg" end
        local _lIOX
        _XIxX.try("grab.confirmAll", function()
            local _XIXo = _lxll and _lxll.ReadFieldEggs and _lxll.ReadFieldEggs()
            for _OXlx, _IlOx in pairs(_XIXo and _XIXo.Records or {}) do
                if _IlOx.State == "Carried" and tostring(_IlOx.Uid) == tostring(_OXXX) then
                    _lIOX = true
                    break
                end
            end
        end)
        if _lIOX then return true, "ReadFieldEggs" end
        return false, _XIXX and _XIXX._XOOo or "unknown"
    end
    local function fireAt(_xoll, _IoOO)
        if not _oOXo.can._xXIO then
            return false, "executor has no fireproximityprompt"
        end
        local _XxOX = _lXxX._oXIX()
        if not _XxOX then return false, "no root" end
        local _IooO = promptList()
        if typeof(_xoll) == "Vector3" then
            _xolx.waitForPrompt(_xoll, _IoOO, _oolx.PROMPT_WAIT)
            if _IoOO and _IoOO() then return false, "cancelled" end
        end
        local _oXoo, _XOOl = nil, math.huge
        for _OXlx, _Ixlx in ipairs(_IooO) do
            if _Ixlx.Parent and _Ixlx.Enabled then
                local _IIXX = promptPos(_Ixlx)
                if _IIXX then
                    local _xool = (typeof(_xoll) ~= "Vector3")
                        or ((_IIXX - _xoll).Magnitude <= _oolx.PROMPT_NEAR)
                    local _xlXo = (_XxOX.Position - _IIXX).Magnitude
                    if _xool and _xlXo <= (_Ixlx.MaxActivationDistance + 8) and _xlXo < _XOOl then
                        _oXoo, _XOOl = _Ixlx, _xlXo
                    end
                end
            end
        end
        if not _oXoo then return false, "no prompt for this egg" end
        local _IIXX = promptPos(_oXoo)
        local _xIlo = (_oXoo.MaxActivationDistance or 8) - _oolx.STEP_INSIDE
        if _IIXX and _XOOl > _xIlo then
            local _ooXo = _XxOX.Position
            local _oIlX = _IIXX - _ooXo
            local _oolX = _IIXX - (_oIlX.Magnitude > 0.1 and _oIlX.Unit or Vector3._oooX(0, 0, 1))
                * math._IOoX(_xIlo * 0.5, 2)
            pcall(function()
                _XxOX.CFrame = CFrame._oooX(Vector3._oooX(_oolX.X, _ooXo.Y, _oolX.Z))
                _XxOX.AssemblyLinearVelocity = Vector3.zero
            end)
            RunService.Heartbeat:Wait()
            local _lIIx = _lXxX._oXIX()
            if _lIIx then _XOOl = (_lIIx.Position - _IIXX).Magnitude end
        end
        local _lXlO, _IIxO = _oXoo.HoldDuration, _oXoo.RequiresLineOfSight
        pcall(function()
            _oXoo.HoldDuration = 0
            _oXoo.RequiresLineOfSight = false
        end)
        local _XOIo = _oOXo.firePrompt(_oXoo, 0)
        if _XOIo then _oOXo.firePrompt(_oXoo) end
        pcall(function()
            _oXoo.HoldDuration = _lXlO
            _oXoo.RequiresLineOfSight = _IIxO
        end)
        return _XOIo and true or false,
            _XOIo and ("fired at %.1f studs"):format(_XOOl)
            or "fireproximityprompt failed",
            _XOOl
    end
    local _xOOo = { attempts = 0, _xoOo = 0, _oxOO = 0, _oxx = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.take(_OXXX, _Xxxo)
        _Xxxo = _Xxxo or {}
        local _IoOO = _Xxxo._IoOO
        local _OxOo  = _Xxxo._OxOo or _oolx.TRIES
        local _xoll = _Xxxo._IIXX
        _xOOo.attempts = _xOOo.attempts + 1
        local _Ollx = _loIx.clock()
        local _lIxo = _lXxX.humanoid()
        local _OlOO = (_lIxo and _lIxo.WalkSpeed and _lIxo.WalkSpeed > 0) and _lIxo.WalkSpeed or nil
        local _lIlx = _XIxX.scope("features.grab.attempt")
        local _IoO = false
        if _lxll and _lxll.CarryChanged then
            _XIxX.try("grab.watchCarry", function()
                _lIlx:connect(_lxll.CarryChanged, function(_XIxo)
                    if type(_XIxo) ~= "table" or _XIxo.Uid == nil
                       or tostring(_XIxo.Uid) == tostring(_OXXX) then
                        _IoO = true
                    end
                end)
            end)
        end
        local function finish(_xOIx, _XIXO, _xXXl, _OIol)
            _lIlx:destroy()
            local _oOIx = (_loIx.clock() - _Ollx) * 1000
            if _xOIx then
                _xOOo._xoOo = _xOOo._xoOo + 1
                _OOXo.markStolen(_OXXX)
            elseif _XIXO == "cancelled" then
                _xOOo._oxx = _xOOo._oxx + 1
            else
                _xOOo._oxOO = _xOOo._oxOO + 1
            end
            local _XIlo = _xOIx and _oloX._XIxo or _oloX.warn
            _XIlo("%s uid=%s after %d/%d tries in %.0fms (witness=%s dist=%s tier=%s)",
                _xOIx and "TAKEN" or ("FAILED: " .. tostring(_XIXO)),
                tostring(_OXXX), _xXXl or 0, _OxOo, _oOIx, tostring(_XIXO),
                _OIol and string.format("%.1f", _OIol) or "-", _OOOX.tier)
            return _xOIx, {
                _XIXO = _XIXO, attempts = _xXXl or 0,
                _oOIx = _oOIx, _IXOl = _OIol,
            }
        end
        local _xXXo, _oXlO = _xolx.confirm(_OXXX, _OlOO, _IoO)
        if _xXXo then return finish(true, _oXlO, 0) end
        for _xXXl = 1, _OxOo do
            if _IoOO and _IoOO() then return finish(false, "cancelled", _xXXl) end
            if not _lXxX._oXIX() then return finish(false, "no character", _xXXl) end
            local _xOIx, _XOOo = _OOXo.stillTakeable(_OXXX)
            if not _xOIx and not _IoO then
                return finish(false, "egg " .. tostring(_XOOo), _xXXl)
            end
            local _XOIo, _oxXX, _xlXo = fireAt(_xoll, _IoOO)
            if _oxXX == "cancelled" then return finish(false, "cancelled", _xXXl) end
            if _XOIo then
                local _oxXO = _loIx.clock() + _OOOX._oIOo(_oolx.CONFIRM_WINDOW)
                repeat
                    if _IoOO and _IoOO() then return finish(false, "cancelled", _xXXl, _xlXo) end
                    local _OXOX, _xlOx = _xolx.confirm(_OXXX, _OlOO, _IoO)
                    if _OXOX then return finish(true, _xlOx, _xXXl, _xlXo) end
                    RunService.Heartbeat:Wait()
                until _loIx.clock() > _oxXO
            end
            if _xXXl < _OxOo then task.wait(_OOOX._oIOo(_oolx.RETRY_GAP)) end
        end
        local _OXOX, _xlOx = _xolx.confirm(_OXXX, _OlOO, _IoO)
        if _OXOX then return finish(true, _xlOx, _OxOo) end
        return finish(false, "no confirmation", _OxOo)
    end
    function _xolx.warmPrompts()
        local _Ollx = _loIx.clock()
        local _oIOx = #promptList()
        return (_loIx.clock() - _Ollx) * 1000, _oIOx
    end
    function _xolx.clearCache()
        _xXIO, _xIll = nil, 0
    end
    return _xolx
end)
_XIxX.module("features.instant", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _XIXo = _XIxX.require("core.data")
    local _lXxX   = _XIxX.require("core.character")
    local _OOOX  = _XIxX.require("core.device")
    local _OOXo  = _XIxX.require("features.eggs")
    local _lXIo = _XIxX.require("features.guard")
    local _oloX  = _XIxX.require("boot.log").for_module("instant")
    local RunService = _OoXX.RunService
    local _xolx = {}
    local _oolx = {
        TIMEOUT       = 3,     -- V3.1 tpStealTimeout. It was 8, and a refusal then
        RACE_THREADS  = 3,     -- K.CARRY_RACE_THREADS
        RACE_STAGGER  = 0.05,  -- K.CARRY_RACE_STAGGER
        LIFT          = 2,     -- stand this far above the egg record
        PULLBACK_GAP  = 25,
        FREE_CALLS    = 12,    -- unthrottled attempts before we start easing off
        SAME_MSG_GAP  = 0.12,  -- wait between calls once a message repeats
        SAME_MSG_STOP = 30,    -- identical refusals before this attempt gives up
    }
    _xolx._oolx = _oolx
    local _lxll, _lol = _XIXo.eggState(), _XIXo.slotIdentity()
    local function ensureModules()
        if not _lxll then _lxll = _XIXo.eggState() end
        if not _lol then _lol = _XIXo.slotIdentity() end
        _xolx._Xxlo = (_lxll ~= nil and type(_lxll.CarryFieldEgg) == "function")
        return _xolx._Xxlo
    end
    ensureModules()
    if not _xolx._Xxlo then
        _oloX.warn("EggState.CarryFieldEgg unavailable - instant steal disabled until it resolves")
    end
    local _Ixxl = 0
    local _xOOo = { runs = 0, _IIxX = 0, lost = 0, _oxx = 0, calls = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    local function slotKeyFor(_OXXX, _oIOO, _IXoO)
        local _xIoX = nil
        _XIxX.try("instant.slotKey", function()
            if _lol and _lol.LooksLikeFirstAreaUid
               and _lol.LooksLikeFirstAreaUid(_OXXX) then
                _xIoX = _lol.SlotKey(_oIOO, _IXoO)
            end
        end)
        return _xIoX
    end
    function _xolx.take(_OXXX, eggPos, _Xxxo)
        _Xxxo = _Xxxo or {}
        local _IoOO = _Xxxo._IoOO or function() return false end
        if not _xolx._Xxlo and not ensureModules() then return false, { _XIXO = "no CarryFieldEgg" } end
        if typeof(eggPos) ~= "Vector3" then return false, { _XIXO = "no egg position" } end
        local _xxoo = _lXxX.get()
        if not _xxoo then return false, { _XIXO = "no character" } end
        _xOOo.runs = _xOOo.runs + 1
        local _Ollx = _loIx.clock()
        local _xXXO = CFrame._oooX(eggPos.X, eggPos.Y + _oolx.LIFT, eggPos.Z)
        local _ollO = slotKeyFor(_OXXX, _Xxxo._oIOO, _Xxxo._IXoO)
        local _XoOl = _loIx.clock() + _OOOX._oIOo(_Xxxo._xOlO or _oolx.TIMEOUT)
        local _lIlx = _XIxX.scope("features.instant.race")
        _Ixxl = _Ixxl + 1
        local _Ollo = _Ixxl
        local _IIxX, _OxOo, _OIIO = false, 0, nil
        local _OIlO, _IOll = nil, 0
        local _IlOO = false
        _XIxX._XXIO._Ioxo("target_tp")
        _lIlx:spawn("hold", function()
            while not _IIxX and _Ixxl == _Ollo and _loIx.clock() < _XoOl and _lIlx:alive() do
                local _xXlx = _lXxX.get()
                if _xXlx then pcall(function() _xXlx:PivotTo(_xXXO) end) end
                local _Xxlx = _lXxX._oXIX()
                if _Xxlx then
                    _Xxlx.AssemblyLinearVelocity = Vector3.zero
                    _Xxlx.AssemblyAngularVelocity = Vector3.zero
                end
                RunService.Heartbeat:Wait()
            end
        end)
        local _xXxl = _lXIo.waitForServerRelease(_IoOO)
        if _IoOO() then
            _Ixxl = _Ixxl + 1
            _lIlx:destroy()
            _xOOo._oxx = _xOOo._oxx + 1
            return false, { _XIXO = "cancelled", _oOIx = (_loIx.clock() - _Ollx) * 1000 }
        end
        for _xxlx = 1, _oolx.RACE_THREADS do
            _lIlx:spawn("invoke" .. _xxlx, function()
                task.wait((_xxlx - 1) * _oolx.RACE_STAGGER)
                while not _IIxX and not _IlOO and _loIx.clock() < _XoOl and _lIlx:alive() do
                    if _IoOO() then return end
                    _OxOo = _OxOo + 1
                    _xOOo.calls = _xOOo.calls + 1
                    local _xOIx, _OlXX, _IooX = pcall(function()
                        return _lxll.CarryFieldEgg(_OXXX, _ollO)
                    end)
                    if _IooX ~= nil then _OIIO = tostring(_IooX) end
                    if type(_IooX) == "string" and _IooX:lower():find("downed") then
                        local _IOxo = _lXIo.ragdollRemaining()
                        if _IOxo > 0 then task.wait(math.min(_IOxo, 0.25)) end
                    end
                    if not _IIxX and type(_IooX) == "string" then
                        if _IooX == _OIlO then
                            _IOll = _IOll + 1
                        else
                            _OIlO, _IOll = _IooX, 1
                        end
                        if _IOll >= _oolx.SAME_MSG_STOP then
                            _IlOO = true
                            return
                        end
                        if _OxOo > _oolx.FREE_CALLS and _IOll > 1 then
                            task.wait(_oolx.SAME_MSG_GAP)
                        end
                    end
                    if _xOIx and _OlXX == true and not _IIxX then
                        _IIxX = true
                        return
                    end
                    if _IIxX then return end
                    RunService.Heartbeat:Wait()
                end
            end)
        end
        local _oxx = false
        while not _IIxX and not _IlOO and _loIx.clock() < _XoOl do
            if _IoOO() then _oxx = true break end
            RunService.Heartbeat:Wait()
        end
        _Ixxl = _Ixxl + 1
        _lIlx:destroy()
        local _oOIx = (_loIx.clock() - _Ollx) * 1000
        local _lXOX = (function()
            local _Xxlx = _lXxX._oXIX()
            return _Xxlx and (_Xxlx.Position - eggPos).Magnitude or -1
        end)()
        if _oxx then
            _xOOo._oxx = _xOOo._oxx + 1
            _oloX._XIxo("cancelled after %d calls in %.0fms", _OxOo, _oOIx)
            return false, { _XIXO = "cancelled", calls = _OxOo, _oOIx = _oOIx }
        end
        _XIxX._XXIO._Ioxo(_IIxX and "target_landed" or "target_lost")
        if _IIxX then
            _xOOo._IIxX = _xOOo._IIxX + 1
            _OOXo.markStolen(_OXXX)
            _oloX._XIxo("WON uid=%s after %d calls in %.0fms (%d threads, gap %.1f, tier=%s)",
                tostring(_OXXX), _OxOo, _oOIx, _oolx.RACE_THREADS, _lXOX, _OOOX.tier)
            return true, { _XIXO = "instant", calls = _OxOo, _oOIx = _oOIx,
                           _lXOX = _lXOX, _xXxl = _xXxl }
        end
        _xOOo.lost = _xOOo.lost + 1
        local _XIXX = _OOXo.get(_OXXX)
        local _XoX = _lXOX > _oolx.PULLBACK_GAP
        local _olXo = ("localGap=%.1f eggState=%s eggMoved=%s pulledBack=%s%s"):format(
            _lXOX,
            _XIXX and tostring(_XIXX._XOOo) or "gone",
            _XIXX and _XIXX._IIXX and tostring((_XIXX._IIXX - eggPos).Magnitude > 5) or "?",
            tostring(_XoX),
            _IlOO and (" bailed after %d identical refusals"):format(_IOll) or "")
        _oloX.warn("LOST uid=%s after %d calls in %.0fms (%s, last: %s, tier=%s)",
            tostring(_OXXX), _OxOo, _oOIx, _olXo, tostring(_OIIO), _OOOX.tier)
        return false, {
            _XIXO = _OIIO or "no accept",
            calls = _OxOo, _oOIx = _oOIx, _lXOX = _lXOX,
            _XoX = _XoX,
            eggState = _XIXX and _XIXX._XOOo or "gone",
            eggGone = _XIXX == nil,
            _xXxl = _xXxl,
        }
    end
    return _xolx
end)
_XIxX.module("features.plot", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _XIXo = _XIxX.require("core.data")
    local _oloX = _XIxX.require("boot.log").for_module("plot")
    local _xolx = {}
    local _oolx = {
        HOME_TTL = 30,      -- slots can change while connected, so re-resolve
        ARRIVE   = 18,      -- close enough to the plot middle
    }
    _xolx._oolx = _oolx
    local _XOx = _XIXo.plotState()
    local _XOOO, _IoOl, _Oxx = nil, 0, nil
    local function resolve()
        local _IIXX, _xXXX
        if _XOx then
            _XIxX.try("plot.findRespawn", function()
                local _IXxX = _XOx.FindRespawnCFrame and _XOx.FindRespawnCFrame()
                if typeof(_IXxX) == "CFrame" then _IIXX, _xXXX = _IXxX.Position, "PlotState.FindRespawnCFrame" end
            end)
        end
        if not _IIXX and _XOx then
            _XIxX.try("plot.resolveSlot", function()
                local _xxIX = _XOx.ResolveLocalSlot and _XOx.ResolveLocalSlot()
                local _oXlo = _xxIX and workspace:FindFirstChild("Plots")
                local _Ooxo = _oXlo and _oXlo:FindFirstChild(tostring(_xxIX))
                if _Ooxo then
                    local _IXxX = _Ooxo:GetPivot()
                    if typeof(_IXxX) == "CFrame" then _IIXX, _xXXX = _IXxX.Position, "plot " .. tostring(_xxIX) end
                end
            end)
        end
        if not _IIXX then
            _XIxX.try("plot.spawnLocation", function()
                local _XIlx = workspace:FindFirstChildOfClass("SpawnLocation")
                if _XIlx and _XIlx:IsA("BasePart") then
                    _IIXX, _xXXX = _XIlx.Position + Vector3._oooX(0, 4, 0), "SpawnLocation"
                end
            end)
        end
        if not _IIXX then
            _XIxX.try("plot.spawnTarget", function()
                local _xIlx = workspace:FindFirstChild("SpawnTarget", true)
                if _xIlx and _xIlx:IsA("BasePart") then
                    _IIXX, _xXXX = _xIlx.Position + Vector3._oooX(0, 4, 0), "SpawnTarget"
                end
            end)
        end
        return _IIXX, _xXXX
    end
    function _xolx._XxXo()
        local _XooX = _loIx.clock()
        if _XOOO and (_XooX - _IoOl) < _oolx.HOME_TTL then
            return _XOOO, _Oxx
        end
        local _IIXX, _xXXX = resolve()
        if not _IIXX then
            _oloX.error("cannot resolve this player's plot - refusing to deliver "
                .. "(PlotState=%s)", tostring(_XOx ~= nil))
            return nil, "no plot resolved"
        end
        if _xXXX ~= _Oxx then
            _oloX._XIxo("home resolved via %s at %s", _xXXX, tostring(_IIXX))
        end
        _XOOO, _IoOl, _Oxx = _IIXX, _XooX, _xXXX
        return _XOOO, _Oxx
    end
    function _xolx.forget()
        _XOOO, _IoOl = nil, 0
    end
    local _OOlO, _IllX, _ooOo = nil, 0, nil
    function _xolx.safeZone()
        local _XooX = _loIx.clock()
        if _OOlO and (_XooX - _IllX) < _oolx.HOME_TTL then
            return _OOlO, _ooOo
        end
        local _IIXX, _xXXX
        _XIxX.try("plot.spawnLocationZone", function()
            local _XIlx = workspace:FindFirstChildOfClass("SpawnLocation")
            if _XIlx and _XIlx:IsA("BasePart") then
                _IIXX, _xXXX = _XIlx.Position + Vector3._oooX(0, 4, 0), "SpawnLocation"
            end
        end)
        if not _IIXX then
            _XIxX.try("plot.spawnTargetZone", function()
                local _xIlx = workspace:FindFirstChild("SpawnTarget", true)
                if _xIlx and _xIlx:IsA("BasePart") then
                    _IIXX, _xXXX = _xIlx.Position + Vector3._oooX(0, 4, 0), "SpawnTarget"
                end
            end)
        end
        if not _IIXX then
            local _xIOx, _loIX = _xolx._XxXo()
            if _xIOx then _IIXX, _xXXX = _xIOx, "plot fallback (" .. tostring(_loIX) .. ")" end
        end
        if not _IIXX then
            _oloX.error("cannot resolve a safe zone - refusing to deliver")
            return nil, "unresolved"
        end
        if _xXXX ~= _ooOo then
            _oloX._XIxo("safe zone resolved via %s at %s", _xXXX, tostring(_IIXX))
        end
        _OOlO, _IllX, _ooOo = _IIXX, _XooX, _xXXX
        return _OOlO, _ooOo
    end
    function _xolx.forgetSafeZone()
        _OOlO, _IllX = nil, 0
    end
    local _OxO, _xIl = 0, nil
    local _xXIl = {}
    function _xolx.claimedSince(_OlOx)
        return _OxO > (_OlOx or 0), _xIl
    end
    function _xolx.onClaim(_lIlx, _xxIo, _xxxX)
        _xXIl[#_xXIl + 1] = { scope = _lIlx, _xxIo = _xxIo, _xxxX = _xxxX }
    end
    local _lIlx = _XIxX.scope("features.plot")
    local _lxll
    _XIxX.try("plot.resolveEggState", function()
        local _OoIo = _OoXX.ReplicatedStorage:FindFirstChild("EggState", true)
        if _OoIo and _OoIo:IsA("ModuleScript") then _lxll = require(_OoIo) end
    end)
    if _lxll and _lxll.FieldClaimed then
        _XIxX.try("plot.armClaimWatch", function()
            _lIlx:connect(_lxll.FieldClaimed, function(_XIxo)
                _OxO = _loIx.clock()
                _xIl = (type(_XIxo) == "table"
                    and (_XIxo.DisplayName or _XIxo.AssetCategory)) or "egg"
                _oloX._XIxo("CLAIM: server claimed our egg -> %s", tostring(_xIl))
                for _xxlx = #_xXIl, 1, -1 do
                    local _Xolx = _xXIl[_xxlx]
                    if not _Xolx.scope or _Xolx.scope._xIXo then
                        table.remove(_xXIl, _xxlx)
                    else
                        _XIxX.try("plot/" .. _Xolx._xxIo, _Xolx._xxxX, _xIl)
                    end
                end
            end)
        end)
    else
        _oloX.warn("EggState.FieldClaimed unavailable - deliveries cannot be confirmed")
    end
    _xolx._listeners = function() return #_xXIl end
    return _xolx
end)
_XIxX.module("features.regrab", function(_XIxX)
    local _OoXX     = _XIxX.require("core.services")
    local _OOXo    = _XIxX.require("features.eggs")
    local _oxxl = _XIxX.require("features.instant")
    local _lXIo   = _XIxX.require("features.guard")
    local _lXxX      = _XIxX.require("core.character")
    local _OOOX     = _XIxX.require("core.device")
    local _oloX     = _XIxX.require("boot.log").for_module("regrab")
    local RunService = _OoXX.RunService
    local _xolx = {}
    local _oolx = {
        SETTLE      = 0.08,   -- V3.1 K.REGRAB_SETTLE
        WAIT        = 8.0,    -- K.REGRAB_WAIT - how long to wait for it to settle
        POLL        = 0.05,
        TRIES       = 4,      -- K.REGRAB_TRIES
        MAX_PER_STEAL = 2,    -- V3.1 midCarryRegrabs < 2
    }
    _xolx._oolx = _oolx
    local _xOOo = { runs = 0, recovered = 0, banked = 0, _IXXo = 0, _oxOO = 0, _oxx = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    local function settledPos(_OXXX)
        local _IlOx = _OOXo.get(_OXXX)
        if not _IlOx then return nil, nil end
        return _IlOx._IIXX, _IlOx._XOOo
    end
    function _xolx.recover(_OXXX, _Xxxo)
        _Xxxo = _Xxxo or {}
        local _IoOO = _Xxxo._IoOO or function() return false end
        _xOOo.runs = _xOOo.runs + 1
        local _Ollx = _loIx.clock()
        task.wait(_oolx.SETTLE)
        if _IoOO() then
            _xOOo._oxx = _xOOo._oxx + 1
            return false, { _XIXO = "cancelled", recovery = "cancelled" }
        end
        local _XoOl = _loIx.clock() + _OOOX._oIOo(_oolx.WAIT)
        local _IIXX, _XOOo, _IxIX
        repeat
            if _IoOO() then
                _xOOo._oxx = _xOOo._oxx + 1
                return false, { _XIXO = "cancelled", recovery = "cancelled" }
            end
            _IIXX, _XOOo = settledPos(_OXXX)
            if _XOOo == "Claimed" then
                _xOOo.banked = _xOOo.banked + 1
                _oloX._XIxo("drop_recovery=banked uid=%s (the egg was claimed)", tostring(_OXXX))
                return false, { _XIXO = "claimed", recovery = "banked" }
            end
            if _XOOo == nil then
                _xOOo._IXXo = _xOOo._IXXo + 1
                _oloX.warn("drop_recovery=failed uid=%s (record gone)", tostring(_OXXX))
                return false, { _XIXO = "gone", recovery = "failed" }
            end
            if _XOOo == "Slot" or _XOOo == "Dropped" then break end
            if _XOOo ~= _IxIX then
                _IxIX = _XOOo
                _oloX.trace("egg is %s - waiting for it to settle", tostring(_XOOo))
            end
            task.wait(_oolx.POLL)
        until _loIx.clock() > _XoOl
        if _XOOo ~= "Slot" and _XOOo ~= "Dropped" then
            _xOOo._oxOO = _xOOo._oxOO + 1
            _oloX.warn("drop_recovery=failed uid=%s (still %s after %.1fs)",
                tostring(_OXXX), tostring(_XOOo), _loIx.clock() - _Ollx)
            return false, { _XIXO = "never settled (" .. tostring(_XOOo) .. ")",
                            recovery = "failed" }
        end
        for _xXXl = 1, _oolx.TRIES do
            if _IoOO() then
                _xOOo._oxx = _xOOo._oxx + 1
                return false, { _XIXO = "cancelled", recovery = "cancelled" }
            end
            local _OIIX, _xXIX = settledPos(_OXXX)
            if _xXIX == "Claimed" then
                _xOOo.banked = _xOOo.banked + 1
                _oloX._XIxo("drop_recovery=banked uid=%s (claimed on the way)", tostring(_OXXX))
                return false, { _XIXO = "claimed", recovery = "banked" }
            end
            if not _OIIX then
                _xOOo._IXXo = _xOOo._IXXo + 1
                _oloX.warn("drop_recovery=failed uid=%s (record gone on the way)", tostring(_OXXX))
                return false, { _XIXO = "gone", recovery = "failed" }
            end
            local _XxOX = _lXxX._oXIX()
            local _xlIl = _XxOX and (_OIIX - _XxOX.Position).Magnitude or -1
            local _OXOX, _XIxo = _oxxl.take(_OXXX, _OIIX, {
                _IoOO = _IoOO,
                _oIOO = _Xxxo._oIOO, _IXoO = _Xxxo._IXoO,
            })
            if _OXOX then
                _xOOo.recovered = _xOOo.recovered + 1
                _oloX._XIxo("drop_recovery=tp uid=%s attempt %d/%d in %.2fs "
                    .. "(was %.0f studs out, %d calls)",
                    tostring(_OXXX), _xXXl, _oolx.TRIES, _loIx.clock() - _Ollx,
                    _xlIl, _XIxo and _XIxo.calls or -1)
                return true, { recovery = "tp", attempts = _xXXl,
                               _oOIx = (_loIx.clock() - _Ollx) * 1000 }
            end
            if _XIxo and _XIxo._XoX then
                _oloX.warn("drop_recovery=tp_refused uid=%s attempt %d/%d "
                    .. "(landed %.0f studs off, reason=%s)",
                    tostring(_OXXX), _xXXl, _oolx.TRIES,
                    _XIxo._lXOX or -1, tostring(_XIxo._XIXO))
            elseif _XIxo and type(_XIxo._XIXO) == "string"
                and (_XIxo._XIXO:lower():find("get closer", 1, true)
                     or _XIxo._XIXO:lower():find("not currently trusted", 1, true)) then
                _xOOo.rebait = (_xOOo.rebait or 0) + 1
                _oloX._XIxo("drop_recovery=rebait uid=%s (in-knockdown pickup refused: %s, %.2fs)",
                    tostring(_OXXX), _XIxo._XIXO, _loIx.clock() - _Ollx)
                return false, { _XIXO = "knockdown window missed", recovery = "rebait" }
            else
                _oloX.trace("attempt %d/%d: %s (egg %s, %.0f studs)",
                    _xXXl, _oolx.TRIES, tostring(_XIxo and _XIxo._XIXO),
                    tostring(_xXIX), _xlIl)
            end
            task.wait(_OOOX._oIOo(_oolx.POLL))
        end
        _xOOo._oxOO = _xOOo._oxOO + 1
        _oloX.warn("drop_recovery=failed uid=%s after %d attempts in %.2fs",
            tostring(_OXXX), _oolx.TRIES, _loIx.clock() - _Ollx)
        return false, { _XIXO = "no regrab", recovery = "failed" }
    end
    return _xolx
end)
_XIxX.module("features.carry", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _xoxo = _XIxX.require("features.movement")
    local _lOIX = _XIxX.require("features.plot")
    local _OOXo = _XIxX.require("features.eggs")
    local _lXxX   = _XIxX.require("core.character")
    local _OOOX  = _XIxX.require("core.device")
    local _oloX  = _XIxX.require("boot.log").for_module("carry")
    local _xolx = {}
    local _oolx = {
        SPEED      = 500,   -- V3.1 K.CARRY_FLOOR; above it the server voids the egg
        ARRIVE     = 5,     -- V3.1 passes arrive = 5 to the carry arc
        CLAIM_WAIT = 6,     -- how long to wait for the server to claim it
    }
    _xolx._oolx = _oolx
    local _xOOo = { runs = 0, _OIIl = 0, _oxOO = 0, _oxx = 0, lost = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    local function holding(_OXXX)
        local _IlOx = _OOXo.get(_OXXX)
        if not _IlOx then return false, "gone" end
        return _IlOx._XOOo == "Carried", _IlOx._XOOo
    end
    function _xolx._XxXo(_OXXX, _Xxxo)
        _Xxxo = _Xxxo or {}
        local _IIo = _Xxxo._IoOO
        _xOOo.runs = _xOOo.runs + 1
        local _Ollx = _loIx.clock()
        local _XoXO = {}
        local function _IOOo(_oXxo, _xxxX)
            local _IIlx = _loIx.clock()
            local _xOIx, _XIxo = _xxxX()
            _XoXO[#_XoXO + 1] = {
                _oXxo = _oXxo, _oOIx = (_loIx.clock() - _IIlx) * 1000, _xOIx = _xOIx and true or false,
            }
            return _xOIx, _XIxo
        end
        local function report()
            local _lXlo = {}
            for _OXlx, _llOx in ipairs(_XoXO) do
                _lXlo[#_lXlo + 1] = ("%s=%.0fms%s"):format(_llOx._oXxo, _llOx._oOIx, _llOx._xOIx and "" or "!")
            end
            return table.concat(_lXlo, " ")
        end
        local function fail(_oxXX)
            _xOOo._oxOO = _xOOo._oxOO + 1
            _oloX.warn("FAILED %s uid=%s after %.2fs [%s] tier=%s",
                _oxXX, tostring(_OXXX), _loIx.clock() - _Ollx, report(), _OOOX.tier)
            return false, { _XIXO = _oxXX, _XoXO = _XoXO, _Olxl = _loIx.clock() - _Ollx }
        end
        local _OlXo, _xXXX = _lOIX.safeZone()
        if not _OlXo then return fail("no safe zone resolved") end
        if not _lXxX._oXIX() then return fail("no character") end
        local _ooIl, _lOol = 0, true
        local function carryCancel()
            if _IIo and _IIo() then return true end
            local _XooX = _loIx.clock()
            if (_XooX - _ooIl) >= 0.25 then
                _ooIl = _XooX
                _lOol = holding(_OXXX)
            end
            return not _lOol
        end
        local _XlOO = _lXxX._oXIX().Position
        local _IXOl = (Vector3._oooX(_OlXo.X, 0, _OlXo.Z)
            - Vector3._oooX(_XlOO.X, 0, _XlOO.Z)).Magnitude
        _oloX._XIxo("carrying %s to the safe zone via %s (%.0f studs, tier=%s)",
            tostring(_OXXX), tostring(_xXXX), _IXOl, _OOOX.tier)
        local _XXXl, _Iool = _IOOo("arc", function()
            return _xoxo.travel{
                _Xllx = _OlXo, _olOo = _oolx.SPEED, _xIOO = _oolx.ARRIVE,
                _OoOl = true, _IoOO = carryCancel, _ooXX = "carry home",
            }
        end)
        local _ooll, _XOOo = holding(_OXXX)
        if not _ooll then
            _xOOo.lost = _xOOo.lost + 1
            local _IXXo = _lXxX._oXIX()
            local _OXll = _IXXo and (_IXXo.Position - _XlOO).Magnitude or -1
            _oloX.warn("carry ended mid-route: egg is %s after %.0f/%.0f studs (%.2fs)",
                tostring(_XOOo), _OXll, _IXOl, _loIx.clock() - _Ollx)
            return false, {
                _XIXO = "dropped in transit (" .. tostring(_XOOo) .. ")",
                _XoXO = _XoXO, droppedAt = _OXll, _IXOl = _IXOl,
            }
        end
        if _IIo and _IIo() then
            _xOOo._oxx = _xOOo._oxx + 1
            return false, { _XIXO = "cancelled", _XoXO = _XoXO }
        end
        if not _XXXl then
            return fail("could not reach the safe zone ("
                .. tostring(_Iool and _Iool._XIXO) .. ")")
        end
        _IOOo("descend", function()
            return _xoxo.descend("deliver"), nil
        end)
        local _xxx = _loIx.clock()
        local _IIxl = _IOOo("claim", function()
            local _oxXO = _loIx.clock() + _OOOX._oIOo(_oolx.CLAIM_WAIT)
            repeat
                if _IIo and _IIo() then return false, { _XIXO = "cancelled" } end
                local _OXOX = _lOIX.claimedSince(_xxx)
                if _OXOX then return true, { _XIXO = "claimed" } end
                _OoXX.RunService.Heartbeat:Wait()
            until _loIx.clock() > _oxXO
            return false, { _XIXO = "no claim" }
        end)
        if not _IIxl then
            local _xXXo, _xIlx = holding(_OXXX)
            return fail(_xXXo and "arrived but never claimed"
                or ("lost at the door (" .. tostring(_xIlx) .. ")"))
        end
        _xOOo._OIIl = _xOOo._OIIl + 1
        _oloX._XIxo("DELIVERED uid=%s in %.2fs via %s [%s] tier=%s",
            tostring(_OXXX), _loIx.clock() - _Ollx, tostring(_xXXX), report(), _OOOX.tier)
        return true, { _XIXO = "delivered", _XoXO = _XoXO, _Olxl = _loIx.clock() - _Ollx }
    end
    return _xolx
end)
_XIxX.module("features.bait", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _XIXo = _XIxX.require("core.data")
    local _xoxo = _XIxX.require("features.movement")
    local _lXxX   = _XIxX.require("core.character")
    local _OOOX  = _XIxX.require("core.device")
    local _oloX  = _XIxX.require("boot.log").for_module("bait")
    local RunService = _OoXX.RunService
    local _xolx = {}
    local _oolx = {
        AREA_WAIT    = 5,     -- how long to wait for GuardAreas to stream in
        APPROACH     = 1200,  -- speed to the bait egg
        ARRIVE       = 4,
        PICKUP_WAIT  = 3,     -- how long to keep asking for the carry
        REHOPS       = 2,     -- server pull-backs we will answer before giving up
        HIT_WAIT     = 4.0,   -- how long to stand in reach waiting for the hit
        WITNESS_HOLD = 0.35,  -- stay anchored this long after a witness fires
    }
    _xolx._oolx = _oolx
    local _lxll, _lol = _XIXo.eggState(), _XIXo.slotIdentity()
    local _OXo = nil
    function _xolx.firstAreaId(waitFor)
        if _OXo then return _OXo end
        if waitFor then
            local _XoOl = _loIx.clock() + waitFor
            while _loIx.clock() < _XoOl do
                local _IXOo = false
                pcall(function()
                    _IXOo = workspace.__OBJECTS.Areas.GuardAreas:GetChildren()[1] ~= nil
                end)
                if _IXOo then break end
                task.wait(0.2)
            end
        end
        local _oXoo, _oXxO
        _XIxX.try("bait.resolveArea", function()
            for _OXlx, _oXlx in ipairs(workspace.__OBJECTS.Areas.GuardAreas:GetChildren()) do
                local _XXlx = _oXlx:FindFirstChild("Bounds")
                if _XXlx and _XXlx:IsA("BasePart") then
                    local _IOOx = _XXlx.Position.X - _XXlx.Size.X * 0.5
                    if not _oXoo or _IOOx < _oXxO then _oXoo, _oXxO = _oXlx.Name, _IOOx end
                end
            end
        end)
        if _oXoo then
            _OXo = _oXoo
            _oloX._XIxo("first area resolved: %s (leftmost at x=%.0f)", _oXoo, _oXxO)
        else
            _oloX.warn("guard areas have not streamed in - no bait area")
        end
        return _OXo
    end
    local function findGuard(_oIOO)
        if not _oIOO then return nil end
        local _oOxo = workspace:FindFirstChild("_Guards")
        if _oOxo then
            for _OXlx, _oxlx in ipairs(_oOxo:GetChildren()) do
                if _oxlx.Name == _oIOO or _oxlx:GetAttribute("AreaId") == _oIOO then return _oxlx end
            end
        end
        local _oXlx
        pcall(function() _oXlx = workspace.__OBJECTS.Areas.GuardAreas[_oIOO] end)
        return _oXlx and _oXlx:FindFirstChild("Guard") or nil
    end
    local function guardPart(_lXIo)
        if not _lXIo then return nil end
        local _oXIX = _lXIo:FindFirstChild("HumanoidRootPart")
            or _lXIo:FindFirstChild("Collider")
            or _lXIo:FindFirstChild("Head")
        if _oXIX and _oXIX:IsA("BasePart") then return _oXIX end
        local _oXoo
        for _OXlx, _Ixlx in ipairs(_lXIo:GetDescendants()) do
            if _Ixlx:IsA("BasePart") then
                local _XlOx = _Ixlx.Size.X * _Ixlx.Size.Y * _Ixlx.Size.Z
                if not _oXoo or _XlOx > _oXoo._XlOx then _oXoo = { _xIOx = _Ixlx, _XlOx = _XlOx } end
            end
        end
        return _oXoo and _oXoo._xIOx or nil
    end
    local _xOOo = { runs = 0, hits = 0, noEgg = 0, noPickup = 0, noHit = 0, _oxx = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.prime(_Xxxo)
        _Xxxo = _Xxxo or {}
        local _IoOO = _Xxxo._IoOO
        _xOOo.runs = _xOOo.runs + 1
        local _Ollx = _loIx.clock()
        local _oIOO = _xolx.firstAreaId(_oolx.AREA_WAIT)
        if not _oIOO then
            return false, { _XIXO = "no bait area" }
        end
        if not _lxll then _lxll = _XIXo.eggState() _lol = _lol or _XIXo.slotIdentity() end
        if not _lxll then
            _xOOo.noEgg = _xOOo.noEgg + 1
            return false, { _XIXO = "no EggState on this executor" }
        end
        local _XIXX
        _XIxX.try("bait.findEgg", function()
            for _OXlx, _IlOx in pairs(_lxll.ReadFieldEggs().Records) do
                if _IlOx.AreaId == _oIOO and _IlOx.State == "Slot" and _IlOx.BoundsCFrame then
                    _XIXX = _IlOx
                    break
                end
            end
        end)
        if not _XIXX then
            _xOOo.noEgg = _xOOo.noEgg + 1
            local _xoXO = {}
            _XIxX.try("bait.dumpNoEgg", function()
                for _OXlx, _IlOx in pairs(_lxll.ReadFieldEggs().Records) do
                    if _IlOx.AreaId == _oIOO then _xoXO[#_xoXO + 1] = ("%s=%s"):format(tostring(_IlOx.NestId), tostring(_IlOx.State)) end
                end
            end)
            table._lIlX(_xoXO)
            _oloX.warn("no Slot egg in %s | area: %s | untilReset=%s", tostring(_oIOO),
                #_xoXO > 0 and table.concat(_xoXO, " ") or "(no records)",
                tostring(_XIXo.secondsUntilReset() and math.floor(_XIXo.secondsUntilReset())))
            return false, { _XIXO = "no bait egg" }
        end
        local _IIXX = _XIXX.BoundsCFrame.Position
        local _olIO = _loIx.clock()
        _xoxo.travel{ _Xllx = _IIXX, _olOo = _oolx.APPROACH, _xIOO = _oolx.ARRIVE,
                     _OoOl = false, _IoOO = _IoOO, _ooXX = "bait approach" }
        if _IoOO and _IoOO() then
            _xOOo._oxx = _xOOo._oxx + 1
            return false, { _XIXO = "cancelled" }
        end
        local _ollO = nil
        _XIxX.try("bait.slotKey", function()
            if _lol and _lol.LooksLikeFirstAreaUid
               and _lol.LooksLikeFirstAreaUid(_XIXX.Uid) then
                _ollO = _lol.SlotKey(_XIXX.AreaId, _XIXX.NestId)
            end
        end)
        local _OXOX = false
        local _XoOl = _loIx.clock() + _OOOX._oIOo(_oolx.PICKUP_WAIT)
        local _llXO, _OxOo = 0, 0
        local _OIIO = nil
        local _XIXl = _lXxX._oXIX() and _lXxX._oXIX().Position
        while _loIx.clock() < _XoOl and not _OXOX do
            if _IoOO and _IoOO() then
                _xOOo._oxx = _xOOo._oxx + 1
                return false, { _XIXO = "cancelled" }
            end
            local _OxXo = _lXxX._oXIX()
            if not _OxXo then return false, { _XIXO = "no character" } end
            if _XIXl and (_OxXo.Position - _IIXX).Magnitude > 60 and _llXO < _oolx.REHOPS then
                _llXO = _llXO + 1
                _oloX.trace("server pulled us back - hopping again (%d/%d)", _llXO, _oolx.REHOPS)
                _xoxo.travel{ _Xllx = _IIXX, _olOo = _oolx.APPROACH, _xIOO = _oolx.ARRIVE,
                             _OoOl = false, _IoOO = _IoOO, _ooXX = "bait rehop" }
                _XoOl = _loIx.clock() + _OOOX._oIOo(_oolx.PICKUP_WAIT)
            end
            _OxOo = _OxOo + 1
            local _xOIx, _OlXX, _IooX = pcall(function() return _lxll.CarryFieldEgg(_XIXX.Uid, _ollO) end)
            if _xOIx and _OlXX == true then _OXOX = true break end
            if not _xOIx then _OIIO = "error: " .. tostring(_OlXX)
            elseif _IooX ~= nil then _OIIO = tostring(_IooX) end
            RunService.Heartbeat:Wait()
        end
        if _OXOX then _XIxX._XXIO._Ioxo("bait_grab") end
        if not _OXOX then
            _xOOo.noPickup = _xOOo.noPickup + 1
            local _xoXO = {}
            _XIxX.try("bait.dumpStates", function()
                for _OXlx, _IlOx in pairs(_lxll.ReadFieldEggs().Records) do
                    if _IlOx.AreaId == _oIOO then
                        _xoXO[#_xoXO + 1] = ("%s=%s"):format(tostring(_IlOx.NestId), tostring(_IlOx.State))
                    end
                end
            end)
            table._lIlX(_xoXO)
            local _OxXo = _lXxX._oXIX()
            _oloX.warn("could not pick up in %s after %d tries, %d rehops (%.2fs) - last refusal: %s | chose %s (%s) dist=%.0f | area: %s | untilReset=%s",
                tostring(_oIOO), _OxOo, _llXO, _loIx.clock() - _Ollx, tostring(_OIIO),
                tostring(_XIXX.NestId), tostring(_XIXX.Uid), _OxXo and (_OxXo.Position - _IIXX).Magnitude or -1,
                table.concat(_xoXO, " "), tostring(_XIXo.secondsUntilReset() and math.floor(_XIXo.secondsUntilReset())))
            return false, { _XIXO = "no pickup", _OxOo = _OxOo, _llXO = _llXO, _IooX = _OIIO }
        end
        _XIxX._XXIO._Ioxo("guard_contact")
        local _lXIo = findGuard(_oIOO)
        local _IXIo = guardPart(_lXIo)
        if _IXIo then
            local _OIIx = _lXxX._oXIX()
            local _xxoo = _lXxX.get()
            if _OIIx and _xxoo then
                local _IIIx = _xoxo.groundY(_IXIo.Position) or _OIIx.Position.Y
                pcall(function()
                    _xxoo:PivotTo(CFrame._oooX(_IXIo.Position.X, _IIIx, _IXIo.Position.Z))
                end)
            end
        else
            _oloX.warn("no guard found in %s", tostring(_oIOO))
        end
        local _XxOX = _lXxX._oXIX()
        local _llOl = _XxOX and _XxOX.CFrame
        if _XxOX then pcall(function() _XxOX.Anchored = true end) end
        local _oXIo, _xXll = nil, nil
        local _XXxX = _loIx.clock() + _OOOX._oIOo(_oolx.HIT_WAIT)
        while _loIx.clock() < _XXxX do
            if _IoOO and _IoOO() then break end
            local _OIIx = _lXxX._oXIX()
            if not _OIIx then break end
            _OIIx.AssemblyLinearVelocity = Vector3.zero
            _OIIx.AssemblyAngularVelocity = Vector3.zero
            if _llOl then pcall(function() _OIIx.CFrame = _llOl end) end
            local _Ixll = false
            local _IIoX = _lXxX.humanoid()
            if _IIoX and _IIoX:GetState() == Enum.HumanoidStateType.Physics then
                _Ixll = true   -- knocked down
            end
            if not _Ixll then
                local _oXoX, _IlOx = pcall(_lxll.ReadFieldEgg, _XIXX.Uid)
                local _xIlx = _oXoX and type(_IlOx) == "table" and _IlOx.State or nil
                _Ixll = (_xIlx == "Dropped" or _xIlx == "GuardCarried")
            end
            if _Ixll and not _xXll then
                _xXll = _loIx.clock()
                _oloX._XIxo("witness seen @%.3f (+%.3fs into the prime)",
                    _xXll, _xXll - _Ollx)
            end
            if _xXll and (_loIx.clock() - _xXll) >= _oolx.WITNESS_HOLD then
                _XIxX._XXIO._Ioxo("hit_detected")
                _oXIo = _loIx.clock()
                _oloX._XIxo("HIT CONFIRMED @%.3f (+%.3fs into the prime, hold=%.3fs)",
                    _oXIo, _oXIo - _Ollx, _oXIo - _xXll)
                break
            end
            RunService.Heartbeat:Wait()
        end
        do
            local _OIIx = _lXxX._oXIX()
            if _OIIx then pcall(function() _OIIx.Anchored = false end) end
            _XIxX._XXIO._Ioxo("unanchor")
        end
        local _lOlX = _oXIo ~= nil
        if _lOlX then _xOOo.hits = _xOOo.hits + 1 else _xOOo.noHit = _xOOo.noHit + 1 end
        _oloX._XIxo("%s in %s after %.2fs (tries=%d rehops=%d witness=%s tier=%s)",
            _lOlX and "HIT TAKEN" or "no hit", tostring(_oIOO), _loIx.clock() - _Ollx,
            _OxOo, _llXO, _xXll and "yes" or "no", _OOOX.tier)
        return _lOlX, {
            _XIXO = _lOlX and "hit" or "no hit",
            _oIOO = _oIOO, _OxOo = _OxOo, _llXO = _llXO,
            _Olxl = _loIx.clock() - _Ollx,
        }
    end
    return _xolx
end)
_XIxX.module("features.autosteal", function(_XIxX)
    local _OoXX   = _XIxX.require("core.services")
    local _OOOX   = _XIxX.require("core.device")
    local _lXxX    = _XIxX.require("core.character")
    local _xIlx    = _XIxX.require("core.state")
    local _OOXo  = _XIxX.require("features.eggs")
    local _lXXo  = _XIxX.require("features.grab")
    local _xoxo  = _XIxX.require("features.movement")
    local _oxxO = _XIxX.require("features.carry")
    local _Xooo  = _XIxX.require("features.bait")
    local _lOIX  = _XIxX.require("features.plot")
    local _lIOO = _XIxX.require("features.antideath")
    local _lXIo  = _XIxX.require("features.guard")
    local _xxIx     = _XIxX.require("core.restore")
    local _oxxl = _XIxX.require("features.instant")
    local _IlXO = _XIxX.require("features.regrab")
    local _XXIo  = _XIxX.require("features.humanoid")
    local _XIXo  = _XIxX.require("core.data")
    local _llX = _XIxX.require("features.guardwatch")
    local _XooO = _XIxX.require("core.motion")
    local _oloX   = _XIxX.require("boot.log").for_module("autosteal")
    local _xolx = {}
    local _OO = false
    local _lX = {}
    local function setAnimationsLocked(_IoIx)
        local _xxoo = _lXxX.get()
        local _IIoX = _lXxX.humanoid()
        if not _xxoo then return end
        local _xoXl = _xxoo:FindFirstChild("Animate")
        if _IoIx then
            if _OO then return end
            _OO = true
            _lX._xoXl = _xoXl
            _lX.disabled = _xoXl and _xoXl.Disabled or false
            if _xoXl then pcall(function() _xoXl.Disabled = true end) end
            if _IIoX then
                local _OlOl = _IIoX:FindFirstChildOfClass("Animator")
                if _OlOl then
                    for _OXlx, track in ipairs(_OlOl:GetPlayingAnimationTracks()) do
                        pcall(function() track:Stop(0) end)
                    end
                end
            end
        else
            if not _OO then return end
            _OO = false
            if _xoXl and _xoXl.Parent then
                pcall(function() _xoXl.Disabled = _lX.disabled end)
            end
            table._lIIo(_lX)
        end
    end
    function _xolx.setAnimationLocked(_IoIx) setAnimationsLocked(_IoIx and true or false) end
    local _OOl = 1.0
    local _IlO  = 8.0
    local _lOx = 0.4
    local _Xo = 2.0   -- inventory full / field resetting only
    local _xoo = 30
    local _Oo = "egg inventory full"
    local _xOo = "waiting for the guard to go home"
    local _Ill = nil
    local _lxxl = nil
    local function isInventoryFull(_IooX)
        return type(_IooX) == "string" and _IooX:lower():find("inventory is full", 1, true) ~= nil
    end
    local _lXo  = "movement not trusted by the server - cooling down"
    local _IoXl     = "no bait egg in the Forest"
    local _XxlO      = "egg back in its nest - re-baiting"
    local _IOO, _Xox = 10, 60
    local _xIx, _oXll = 0, 0
    local function isTrustRefusal(_IooX)
        if type(_IooX) ~= "string" then return false end
        local _OIOx = _IooX:lower()
        return _OIOx:find("not currently trusted", 1, true) ~= nil
            or _OIOx:find("get closer", 1, true) ~= nil
    end
    local function distrust(_oxXX)
        _oXll = math.min(math._IOoX(_oXll * 2, _IOO), _Xox)
        _xIx = _loIx.clock() + _oXll
        _oloX.warn("server refused our movement (%s) - no teleports for %.0fs", tostring(_oxXX), _oXll)
    end
    function _xolx.trustCooldown() return math._IOoX(0, _xIx - _loIx.clock()), _oXll end
    local _lIoo = { _OXXX = nil, _IooX = nil, _IIlO = 0, phase = nil, phaseAt = 0, reported = nil,
                    passAt = 0 }
    _xolx.STATE = {
        PREP_DELIVER_HELD = "PREP_DELIVER_HELD",
        READY_TO_STEAL    = "READY_TO_STEAL",
        BAIT_NOT_DONE     = "BAIT_NOT_DONE",
        BAIT_DONE         = "BAIT_DONE",
        AT_TARGET         = "AT_TARGET",
        TARGET_GRAB_RETRY = "TARGET_GRAB_RETRY",
        CARRYING          = "CARRYING",
        RETURNING         = "RETURNING",
        DELIVERED         = "DELIVERED",
    }
    local _OxoO = {}
    local _IXol = 0
    local function phase(_oXOo, _oXxo, _XXOO)
        if _oXOo ~= _IXol then
            _OxoO, _IXol = {}, _oXOo
        end
        if _XXOO == nil and _OxoO[#_OxoO] == _oXxo then return end
        if _lIoo.phase ~= _oXxo then
            _lIoo.phase, _lIoo.phaseAt, _lIoo.reported = _oXxo, _loIx.clock(), nil
        end
        _OxoO[#_OxoO + 1] = _oXxo
        if #_OxoO > 200 then table.remove(_OxoO, 1) end
        _oloX._XIxo("run %d: phase %s%s", _oXOo, _oXxo,
            _XXOO and (" (" .. tostring(_XXOO) .. ")") or "")
    end
    function _xolx._OxoO() return table._OIIo(_OxoO) end
    local _xo = 2
    local _xOl = 12
    local _IOl = {}
    function _xolx.onStop(_xxxX)
        _IOl[#_IOl + 1] = _xxxX
    end
    local _xx = nil
    function _xolx.setBetweenCycles(_xxxX) _xx = _xxxX end
    local _XIl = {}
    function _xolx.onIdle(_xxxX)
        _XIl[#_XIl + 1] = _xxxX
    end
    local _x = {}
    function _xolx.onDelivered(_xxxX)
        _x[#_x + 1] = _xxxX
    end
    local _ol = {}
    function _xolx.onCarrying(_xxxX)
        _ol[#_ol + 1] = _xxxX
    end
    local function fireCarrying(_xXXO)
        if not _xXXO then return end
        for _OXlx, _xxxX in ipairs(_ol) do
            task.spawn(function() _XIxX.try("autosteal.onCarrying", _xxxX, _xXXO) end)
        end
    end
    local function fireDelivered(_xXXO)
        if not _xXXO then return end
        for _OXlx, _xxxX in ipairs(_x) do
            task.spawn(function() _XIxX.try("autosteal.onDelivered", _xxxX, _xXXO) end)
        end
    end
    local _oxol = 0
    local _lIlO  = false
    local _OXOO   = 0
    local _lIlx       = nil
    local _xxOl = 0
    local _Xxxo     = {}       -- the live run's options
    local _oOIO  = {}       -- source -> that tab's options
    local _Xolo    = nil      -- which source started the live run
    local function snapshot()
        local _Xxlx = _XIxX._XXIO._xIoO()
        local _lxlx = _OOXo._xOOo()
        return {
            _lOXO = _Xxlx._lOXO, _XIIo = _Xxlx._XIIo, _XxIo = _Xxlx._XxIo, _XOlO = _Xxlx._XOlO,
            eggList = _lxlx.listSize, eggValues = _lxlx._llx,
        }
    end
    local _Iox = { "scopes", "conns", "insts", "threads", "eggList", "eggValues" }
    local function _XlXo(_oXlx, _XXlx)
        local _lxoX = {}
        for _OXlx, _IIOx in ipairs(_Iox) do
            local _Ixlx = (_XXlx[_IIOx] or 0) - (_oXlx[_IIOx] or 0)
            if _Ixlx ~= 0 then _lxoX[#_lxoX + 1] = ("%s %+d"):format(_IIOx, _Ixlx) end
        end
        return #_lxoX > 0 and table.concat(_lxoX, " ") or "no change"
    end
    local function runCycle(_oXOo, _IoOO)
        local _IlIo = { _Ollx = _loIx.clock(), _XoXO = {} }
        _lIoo.passAt = _IlIo._Ollx
        _lIoo._OXXX, _lIoo._IooX, _lIoo._IIlO = nil, nil, 0
        if _loIx.clock() < _xIx then
            return false, _lXo, _IlIo
        end
        _XIxX._XXIO._Ioxo("cycle_start")
        local function _IOOo(_oXxo, _xxxX)
            if _IoOO() then return false, { _XIXO = "cancelled" } end
            local _IIlx = _loIx.clock()
            local _xOIx, _XIxo = _xxxX()
            _IlIo._XoXO[#_IlIo._XoXO + 1] = {
                _oXxo = _oXxo, _oOIx = (_loIx.clock() - _IIlx) * 1000, _xOIx = _xOIx and true or false,
            }
            return _xOIx, _XIxo
        end
        local _lxXo = _OOXo.carryingUid()
        if _lxXo then
            local _lxO = (_Xxxo._OXXX ~= nil) and (_lxXo == _Xxxo._OXXX)
            _IlIo.prep = not _lxO
            _IlIo._XOOo = _lxO and _xolx.STATE.RETURNING
                or _xolx.STATE.PREP_DELIVER_HELD
            phase(_oXOo, _IlIo._XOOo, "holding " .. tostring(_lxXo))
            _IlIo.recovered = _lxXo
            _oloX._XIxo("already carrying %s - %s", _lxXo,
                _lxO and "this is the selected egg, delivering to finish"
                or "not the selected egg, clearing our hands first")
            local _lXoX, _OxIo = _IOOo("carry held", function()
                return _oxxO._XxXo(_lxXo, { _IoOO = _IoOO })
            end)
            if _lXoX then
                _IlIo._xXXO = { _oXxo = _lxO and "selected egg" or "held egg",
                                 _OXXX = _lxXo }
                if _lxO then
                    _IlIo._XOOo = _xolx.STATE.DELIVERED
                    _IlIo.terminal = true
                    phase(_oXOo, _IlIo._XOOo, _lxXo)
                    return true, "delivered", _IlIo
                end
                _IlIo._XOOo = _xolx.STATE.READY_TO_STEAL
                _IlIo.terminal = false
                phase(_oXOo, _IlIo._XOOo, "hands clear after prep")
                return true, "prep: held egg delivered", _IlIo
            end
            return false, "held egg: " .. tostring(_OxIo and _OxIo._XIXO), _IlIo
        end
        if _IlIo._XOOo == nil then
            _IlIo._XOOo = _xolx.STATE.READY_TO_STEAL
            phase(_oXOo, _IlIo._XOOo)
        end
        if _XIXo.fieldSealed() then
            return false, "field resetting", _IlIo
        end
        local _Ilx = _XIXo.secondsUntilReset()
        if _Ilx and _Ilx < _xoo then
            return false, "field resetting", _IlIo
        end
        local _Xxxl, _xlol, _IOol = _XIXo.eggInventory()
        if _Xxxl then
            _IlIo.inventory = ("%d/%d"):format(_xlol, _IOol)
            return false, _Oo, _IlIo
        end
        _lxxl = nil
        local _XIll = nil
        local _oIl = false
        if _Xxxo._OXXX and not _OOXo.get(_Xxxo._OXXX) then
            return false, "selected egg is gone", _IlIo
        end
        if _Xxxo._OlIX and not _Xxxo._OXXX then
            local _XOlo, _lIXX, _oIxO, _XOIO = pcall(_Xxxo._OlIX)
            _oIl = _XOlo and _XOIO == true
            if not _XOlo then
                return false, "target picker failed: " .. tostring(_lIXX), _IlIo
            end
            if not _lIXX then
                return false, "nothing to steal"
                    .. (_oIxO and (" (" .. tostring(_oIxO) .. ")") or ""), _IlIo
            end
            _XIll = _lIXX
        end
        do
            local _xxlX = _Xxxo._OXXX and _OOXo.get(_Xxxo._OXXX) or _XIll
            local _XXx = _xxlX and not _oIl and _llX.blocking(_xxlX._oIOO, _xxlX._IIXX)
            if _XXx then
                _IlIo.guardWait = _XXx
                if _XXx ~= _Ill then
                    _Ill = _XXx
                    _oloX._XIxo("holding the steal: %s", _XXx)
                end
                return false, _xOo, _IlIo
            end
            _Ill = nil
        end
        local _olIl = _Xooo.firstAreaId(0)
        local _xlX = nil
        if _Xxxo._OXXX then
            local _oolX = _OOXo.get(_Xxxo._OXXX)
            _xlX = _oolX and _olIl and _oolX._oIOO == _olIl or false
        elseif _XIll then
            _xlX = _olIl ~= nil and _XIll._oIOO == _olIl
        end
        local _IIXO = false
        if _xlX then
            _oloX._XIxo("target is in the bait area (%s) - not priming, going straight for it (V3.1 rule)",
                tostring(_olIl))
            _IlIo.baitSkipped = true
        else
            local _OOOl
            _IIXO, _OOOl = _IOOo("bait", function()
                return _Xooo.prime({ _IoOO = _IoOO })
            end)
            if not _IIXO and _OOOl and isInventoryFull(_OOOl._IooX) then
                return false, _Oo, _IlIo
            end
            if not _IIXO and _OOOl then
                local _IlOx = _OOOl._XIXO
                _lIoo._IooX = _OOOl._IooX or _IlOx
                if _IoOO() then return false, "cancelled", _IlIo end
                if _IlOx == "no pickup" and isTrustRefusal(_OOOl._IooX) then
                    distrust("bait pickup: " .. tostring(_OOOl._IooX))
                    return false, _lXo, _IlIo
                elseif _IlOx == "no bait egg" then
                    return false, _IoXl, _IlIo
                elseif _IlOx == "no pickup" or _IlOx == "no hit" then
                    return false, "bait not taken (" .. tostring(_IlOx)
                        .. (_OOOl._IooX and (": " .. tostring(_OOOl._IooX)) or "") .. ")", _IlIo
                end
            end
        end
        _IlIo._IIXO = _IIXO and true or false
        if _IoOO() then return false, "cancelled", _IlIo end
        local _xXXO
        if _Xxxo._OXXX then
            local _oolX = _OOXo.get(_Xxxo._OXXX)
            if not _oolX then
                return false, "selected egg is gone", _IlIo
            end
            local _OlXl = (_oolX._XOOo == "Slot" or _oolX._XOOo == "Dropped")
            if not _OlXl or not _oolX._IIXX then
                return false, "waiting for the selected egg (" .. tostring(_oolX._XOOo) .. ")", _IlIo
            end
            _xXXO = _oolX
        elseif _Xxxo._OlIX then
            local _lXoX, _oolX, _xolX = true, _XIll, nil
            if not (_IlIo.baitSkipped and _XIll) then
                _lXoX, _oolX, _xolX = pcall(_Xxxo._OlIX)
            end
            if not _lXoX then
                return false, "target picker failed: " .. tostring(_oolX), _IlIo
            end
            _xXXO = _oolX
            if not _xXXO then
                return false, "nothing matches the filter"
                    .. (_xolX and (" (" .. tostring(_xolX) .. ")") or ""), _IlIo
            end
        else
            _xXXO = _OOXo._oXoo()
        end
        if not _xXXO then return false, "nothing to steal", _IlIo end
        _IlIo._xXXO = _xXXO
        _lIoo._OXXX = _xXXO._OXXX
        local _OxXo = _lXxX._oXIX()
        _IlIo._IXOl = _OxXo and (_xXXO._IIXX - _OxXo.Position).Magnitude or -1
        _IlIo._XOOo = _xolx.STATE.BAIT_DONE
        phase(_oXOo, _IlIo._XOOo, _IlIo._IIXO and "primed"
            or (_IlIo.baitSkipped and "bait skipped: target in the bait area" or "no bait egg"))
        _oloX._XIxo("target uid=%s name=%s area=%s rarity=%s state=%s dist=%.0f primed=%s",
            tostring(_xXXO._OXXX), tostring(_xXXO._oXxo), tostring(_xXXO._oIOO),
            tostring(_xXXO._lIXO), tostring(_xXXO._XOOo), _IlIo._IXOl or -1,
            tostring(_IlIo._IIXO))
        local _lOlX, _oloO
        local _IIlO = 0
        for _xXXl = 0, _xo do
            _IlIo._XOOo = (_xXXl == 0) and _xolx.STATE.AT_TARGET or _xolx.STATE.TARGET_GRAB_RETRY
            phase(_oXOo, _IlIo._XOOo, _xXXO._oXxo)
            _lOlX, _oloO = _IOOo(_xXXl == 0 and "instant" or ("regrab" .. _xXXl), function()
                return _oxxl.take(_xXXO._OXXX, _xXXO._IIXX, {
                    _IoOO = _IoOO,
                    _oIOO = _xXXO._oIOO, _IXoO = _xXXO._IXoO,
                })
            end)
            _lIoo._IooX, _lIoo._IIlO = _oloO and _oloO._XIXO, _xXXl
            if _lOlX or _IoOO() then break end
            if _oloO and type(_oloO._XIXO) == "string"
               and _oloO._XIXO:lower():find("not currently trusted", 1, true) then
                break
            end
            local _xIlx = _oloO and _oloO.eggState
            local _Xlll = _oloO and (_oloO._XoX
                or _xIlx == "Slot" or _xIlx == "Dropped")
            if not _Xlll or _xXXl == _xo then break end
            local _XoIo = _OOXo.get(_xXXO._OXXX)
            if not _XoIo or not _XoIo._IIXX then break end
            _xXXO._IIXX = _XoIo._IIXX
            _IIlO = _IIlO + 1
            _oloX._XIxo("target retry %d/%d (reason=%s state=%s pulledBack=%s)",
                _xXXl + 1, _xo,
                tostring(_oloO and _oloO._XIXO), tostring(_xIlx),
                tostring(_oloO and _oloO._XoX))
        end
        _IlIo.grabRetries = _IIlO
        if _IoOO() then return false, "cancelled", _IlIo end
        if _lOlX then
            _IlIo._XOOo = _xolx.STATE.CARRYING
            phase(_oXOo, _IlIo._XOOo, "instant")
            fireCarrying(_xXXO)
            _IlIo.transition = "tp"
            _IlIo.calls = _oloO and _oloO.calls
            _IlIo.tpGap = _oloO and _oloO._lXOX
        else
            _IlIo.transition = "arc_fallback"
            _IlIo.instantFail = _oloO and _oloO._XIXO
            if isInventoryFull(_oloO and _oloO._XIXO) then
                return false, _Oo, _IlIo
            end
            if _oloO and not _oloO._XoX and isTrustRefusal(_oloO._XIXO) then
                distrust("target pickup: " .. tostring(_oloO._XIXO))
                return false, _lXo, _IlIo
            end
            _IlIo.instantDiag = _oloO
            local _lxIO, _Iool = _IOOo("approach", function()
                return _xoxo.travel{
                    _Xllx = _xXXO._IIXX, _olOo = _xoxo.outboundSpeed(),
                    _xIOO = 4, _OoOl = false, _IoOO = _IoOO, _ooXX = "approach",
                }
            end)
            if _IoOO() then return false, "cancelled", _IlIo end
            if not _lxIO then
                return false, "approach: " .. tostring(_Iool and _Iool._XIXO), _IlIo
            end
            local _Xoxl, _llol = _IOOo("grab", function()
                return _lXXo.take(_xXXO._OXXX, { _IIXX = _xXXO._IIXX, _IoOO = _IoOO })
            end)
            if _IoOO() then return false, "cancelled", _IlIo end
            if not _Xoxl then
                _OOXo.markUnreachable(_xXXO._OXXX)
                return false, "grab: " .. tostring(_llol and _llol._XIXO), _IlIo
            end
            _IlIo._XOOo = _xolx.STATE.CARRYING
            phase(_oXOo, _IlIo._XOOo, "prompt")
            fireCarrying(_xXXO)
        end
        _IlIo._XOOo = _xolx.STATE.RETURNING
        phase(_oXOo, _IlIo._XOOo, _xXXO._oXxo)
        local _OIIl, _Xxx = _IOOo("carry", function()
            return _oxxO._XxXo(_xXXO._OXXX, { _IoOO = _IoOO })
        end)
        local _oXX = 0
        while not _OIIl and not _IoOO()
              and _Xxx and _Xxx._XIXO
              and tostring(_Xxx._XIXO):find("dropped in transit", 1, true)
              and _oXX < _IlXO._oolx.MAX_PER_STEAL do
            _OoXX.RunService.Heartbeat:Wait()
            _oXX = _oXX + 1
            _IlIo._oXX = _oXX
            _IlIo._XOOo = _xolx.STATE.TARGET_GRAB_RETRY
            local _oooo, _xxlo = _IOOo("recover" .. _oXX, function()
                return _IlXO.recover(_xXXO._OXXX, {
                    _IoOO = _IoOO,
                    _oIOO = _xXXO._oIOO, _IXoO = _xXXO._IXoO,
                })
            end)
            _IlIo.dropRecovery = _xxlo and _xxlo.recovery or "?"
            if not _oooo then
                if _xxlo and _xxlo.recovery == "rebait" then
                    return false, _XxlO, _IlIo
                end
                return false, "drop recovery: " .. tostring(_xxlo and _xxlo._XIXO), _IlIo
            end
            _IlIo._XOOo = _xolx.STATE.RETURNING
            _OIIl, _Xxx = _IOOo("carry" .. _oXX, function()
                return _oxxO._XxXo(_xXXO._OXXX, { _IoOO = _IoOO })
            end)
        end
        if _IoOO() then return false, "cancelled", _IlIo end
        if not _OIIl then
            return false, "carry: " .. tostring(_Xxx and _Xxx._XIXO), _IlIo
        end
        _IlIo._XOOo = _xolx.STATE.DELIVERED
        _IlIo.terminal = true
        phase(_oXOo, _IlIo._XOOo, _xXXO._oXxo)
        _oXll = 0
        setAnimationsLocked(false)
        fireDelivered(_xXXO)
        return true, "delivered", _IlIo
    end
    local function reportCycle(_xOIx, _oxXX, _IlIo, _XlOO, _oOxO)
        local _lXlo = {}
        for _OXlx, _llOx in ipairs(_IlIo._XoXO) do
            _lXlo[#_lXlo + 1] = ("%s=%.0fms%s"):format(_llOx._oXxo, _llOx._oOIx, _llOx._xOIx and "" or "!")
        end
        if not _xOIx then
            local _lllo = _XIxX._XXIO.marksSince(_IlIo._Ollx)
            if #_lllo > 0 then
                _oloX.warn("timeline: %s", table.concat(_lllo, " | "))
            end
        end
        local _XIlo = _xOIx and _oloX._XIxo or _oloX.warn
        _XIlo("cycle %s in %.2fs [%s] target=%s dist=%.0f %s | %s",
            _xOIx and "DELIVERED" or ("FAILED " .. tostring(_oxXX)),
            _loIx.clock() - _IlIo._Ollx, table.concat(_lXlo, " "),
            _IlIo._xXXO and _IlIo._xXXO._oXxo or "-",
            _IlIo._IXOl or -1,
            ("state=%s transition=%s calls=%s retries=%d recoveries=%d%s primed=%s%s"):format(
                _IlIo._XOOo or "?", _IlIo.transition or "?",
                tostring(_IlIo.calls or "-"), _IlIo.grabRetries or 0,
                _IlIo._oXX or 0,
                _IlIo.dropRecovery and (" drop_recovery=" .. _IlIo.dropRecovery) or "",
                tostring(_IlIo._IIXO),
                _IlIo.instantFail and (" instantFail=" .. tostring(_IlIo.instantFail)
                    .. " pulledBack=" .. tostring(_IlIo.instantDiag and _IlIo.instantDiag._XoX)
                    .. " eggState=" .. tostring(_IlIo.instantDiag and _IlIo.instantDiag.eggState)) or ""),
            _XlXo(_XlOO, _oOxO))
    end
    local _OOx = 3
    local _OlO = 6
    local _oxO = nil
    local _XIx = _XIxX._XXIO.wrapLoop("features.autosteal/pass", _lOx, runCycle)
    local function runLoop(_oXOo)
        _oloX._XIxo("run %d: begin (tier=%s)", _oXOo, _OOOX.tier)
        phase(_oXOo, "START", "tier=" .. tostring(_OOOX.tier))
        local _xXlo = 0
        local _IlX = 0
        _oxO = nil
        local _IxO = function()
            return (not _lIlO) or _oXOo ~= _oxol or (not _XIxX.alive())
        end
        while _lIlO and _oXOo == _oxol and _XIxX.alive() do
            _OoXX.RunService.Heartbeat:Wait()
            if not _lIlO or _oXOo ~= _oxol then break end
            local _XlOO = snapshot()
            local _xOIx, _oxXX, _IlIo = _XIx(_oXOo, _IxO)
            local _oOxO = snapshot()
            if _oxXX ~= "selected egg is gone" then _IlX = 0 end
            local _oIxo = type(_oxXX) == "string"
                and (_oxXX:find("^nothing to steal") or _oxXX:find("^nothing matches the filter")
                    or _oxXX == "field resetting" or _oxXX == _Oo or _oxXX == _xOo
                    or _oxXX == _lXo or _oxXX == _IoXl
                    or _oxXX == "selected egg is gone") or false
            if _oIxo then
                _lxxl = _oxXX
                if _oxXX ~= _oxO then
                    _oxO = _oxXX
                    _oloX._XIxo("idle: %s", _oxXX)
                    local _XXOO = _oxXX
                    if _oxXX == _Oo then
                        local _OXlx, _oIOx, _lloX = _XIXo.eggInventory()
                        if _oIOx and _lloX then _XXOO = ("%s (%d/%d)"):format(_oxXX, _oIOx, _lloX) end
                    end
                    for _OXlx, _xxxX in ipairs(_XIl) do
                        task.spawn(function() _XIxX.try("autosteal.onIdle", _xxxX, _XXOO, _Xolo) end)
                    end
                end
            else
                _oxO, _lxxl = nil, nil
                if _IlIo then reportCycle(_xOIx, _oxXX, _IlIo, _XlOO, _oOxO) end
            end
            if _oxXX == "cancelled" then break end
            if _xOIx and not (_IlIo and _IlIo.terminal) then
                _xxOl = 0
                _xXlo = _xXlo + 1
                if _xXlo > _OOx then
                    _oloX.warn("%d preparation passes without a steal - stopping",
                        _xXlo)
                    return "ended"
                end
                _oloX._XIxo("preparation complete (%s) - continuing the same run",
                    tostring(_oxXX))
            elseif _xOIx and _Xxxo.continuous then
                _xxOl = 0
                _OXOO = _OXOO + 1
                _oloX._XIxo("delivered (%d this run) - continuing", _OXOO)
                if _xx and _lIlO and _oXOo == _oxol then
                    _XIxX.try("autosteal.betweenCycles", _xx, _Xolo)
                end
            elseif _xOIx then
                _xxOl = 0
                _OXOO = _OXOO + 1
                _oloX._XIxo("delivered - run complete")
                return "delivered"
            elseif _oxXX == "selected egg is gone" then
                _IlX = _IlX + 1
                if _IlX >= _OlO then
                    _oloX._XIxo("selected egg is gone (%d checks) - stopping", _IlX)
                    return "selected egg is gone"
                end
                task.wait(_OOOX._oIOo(_lOx))
            elseif _oxXX == _XxlO then
                _xxOl = 0
                _oloX._XIxo("guard returned the egg to its nest - re-baiting now")
            elseif _oxXX == _lXo then
                task.wait(math._IOoX(_lOx, _xIx - _loIx.clock()))
            elseif _oxXX == _Oo or _oxXX == "field resetting" or _oxXX == _IoXl then
                task.wait(_OOOX._oIOo(_Xo))
            elseif (type(_oxXX) == "string" and _oxXX:find("^nothing to steal"))
                or _oxXX == "nothing matches the filter"
                or (type(_oxXX) == "string" and _oxXX:find("^nothing matches the filter"))
                or _oxXX == "field resetting" or _oxXX == _Oo or _oxXX == _xOo
                or (type(_oxXX) == "string" and _oxXX:find("waiting for the selected egg", 1, true)) then
                task.wait(_OOOX._oIOo(_lOx))
            else
                _xxOl = _xxOl + 1
                local wait = math.min(_OOl * (2 ^ (_xxOl - 1)), _IlO)
                wait = _OOOX._oIOo(wait)
                _oloX.warn("backing off %.1fs (failure %d)", wait, _xxOl)
                task.wait(wait)
            end
        end
        _oloX._XIxo("run %d: ended", _oXOo)
        return "ended"
    end
    local function _XIlX(_XIXO)
        if not _lIlO then return end
        _lIlO = false
        _oxol = _oxol + 1
        _xIlx.autoStealOn = false
        _XooO.release("autosteal")
        if _lIlx then
            _lIlx:destroy()
            _lIlx = nil
        end
        _xxOl = 0
        local _oIoo = _Xolo
        _Xolo = nil
        _Xxxo = {}
        _XIxX.try("autosteal.antideath", _lIOO.disarm)
        _XIxX.try("autosteal.humanoid", _XXIo.disarm)
        _XIxX.try("autosteal.guard", _lXIo.disarm)
        _XIxX.try("autosteal.resetMovement", _xoxo.reset)
        _XIxX.try("autosteal.unanchor", function()
            local _XxOX = _lXxX._oXIX()
            if _XxOX and _XxOX.Anchored then _XxOX.Anchored = false end
        end)
        local _Ixol, _OllO, _oxOO = 0, 0, 0
        _XIxX.try("autosteal.restore", function()
            _Ixol, _OllO, _oxOO = _xxIx.restoreAll()
        end)
        local _oXIl = {}
        _XIxX.try("autosteal.audit", function() _oXIl = _xxIx.audit() end)
        if #_oXIl == 0 and _oxOO == 0 then
            _oloX._XIxo("autosteal cleanup: PASS (%d restored, %d skipped)",
                _Ixol, _OllO)
        else
            _oloX.warn("autosteal cleanup: %d restored, %d skipped, %d FAILED%s",
                _Ixol, _OllO, _oxOO,
                #_oXIl > 0
                    and (" | still modified: " .. table.concat(_oXIl, "; ")) or "")
        end
        _oloX._XIxo("stopped (%s) after %d cycles", _XIXO or "requested", _OXOO)
        phase(_IXol, "STOP", _XIXO or "requested")
        _oloX._XIxo("run %d trail: %s", _IXol, table.concat(_OxoO, " -> "))
        local _oxXX = _XIXO or "requested"
        for _OXlx, _xxxX in ipairs(_IOl) do
            task.spawn(function() _XIxX.try("autosteal.onStop", _xxxX, _oxXX, _oIoo) end)
        end
    end
    function _xolx.capability()
        local _oOXo = _XIxX.require("core.exec")
        local _OXlo = {}
        if _oxxl._Xxlo then _OXlo[#_OXlo + 1] = "instant (CarryFieldEgg)" end
        if _oOXo.can._xXIO then _OXlo[#_OXlo + 1] = "prompt (" .. tostring(_oOXo.promptVia) .. ")" end
        if #_OXlo == 0 then
            return false, "Auto Steal cannot run on this executor: no game-module require ("
                .. tostring(_oOXo.gameRequireWhy) .. ") and no proximity prompt path"
        end
        return true, table.concat(_OXlo, " + ")
    end
    local function _oOOo(_oOXX)
        if _lIlO then return end
        local _IOlo, _loOO = _xolx.capability()
        if not _IOlo then
            _oloX.error("%s", _loOO)
            return false, _loOO
        end
        _Xolo = tostring(_oOXX or "main")
        _Xxxo = _oOIO[_Xolo] or {}
        _oloX._XIxo("run starting for %s - pickup via %s", _Xolo, _loOO)
        if _lIlx then _lIlx:destroy() end
        _oxol = _oxol + 1
        _lIlO  = true
        _xIlx.autoStealOn = true
        _XooO.claim("autosteal")
        _lIlx = _XIxX.scope("features.autosteal")
        local _oXOo = _oxol
        _lXxX.onSpawn(_lIlx, "autosteal.respawn", function()
            if not _lIlO or _oXOo ~= _oxol then return end
            _xxOl = 0
            _oloX.trace("respawn: run %d continues", _oXOo)
        end)
        local _XoxO = {}
        for _OXlx, _oXlx in ipairs({ { "humanoid", _XXIo.arm }, { "guard", _lXIo.arm },
                             { "antideath", _lIOO.arm } }) do
            local _xOIx = _XIxX.try("autosteal.arm." .. _oXlx[1], _oXlx[2])
            _XoxO[#_XoxO + 1] = _oXlx[1] .. (_xOIx and "=ok" or "=FAILED")
        end
        _oloX._XIxo("run %d: armed %s", _oXOo, table.concat(_XoxO, " "))
        _lIoo.phase, _lIoo.phaseAt, _lIoo.reported, _lIoo.passAt = nil, _loIx.clock(), nil, _loIx.clock()
        local _xIxO
        _xIxO = _lIlx:spawn("loop", function()
            _oloX._XIxo("run %d: worker thread started (owner=%s, options: %s)",
                _oXOo, tostring(_Xolo),
                _Xxxo._OXXX and ("uid=" .. tostring(_Xxxo._OXXX))
                    or (_Xxxo._OlIX and ("picker" .. (_Xxxo.continuous and ", continuous" or ""))
                        or "best value"))
            local _XIXO = runLoop(_oXOo)
            if _oXOo == _oxol then
                if _XIXO == "delivered" then
                    _XIlX("delivered")
                elseif _lIlO then
                    _XIlX(_XIXO or "ended")
                end
            end
        end)
        local _XlxO = { PREP_DELIVER_HELD = 40, READY_TO_STEAL = 30, BAIT_DONE = 12,
                        AT_TARGET = 10, TARGET_GRAB_RETRY = 25, CARRYING = 5, RETURNING = 35 }
        _lIlx:loop("watchdog", 1, function()
            if not _lIlO or _oXOo ~= _oxol then return end
            local _XooX = _loIx.clock()
            local _oxxo, _IXXO = pcall(coroutine._IXXO, _xIxO)
            if _oxxo and _IXXO == "dead" and _lIlO and _oXOo == _oxol then
                _oloX.error("run %d: worker thread is dead while the run is on - stopping cleanly", _oXOo)
                task.spawn(_XIlX, "worker died")
                return
            end
            local _IXIx = _lIoo.phase
            local _xIlo = _IXIx and _XlxO[_IXIx]
            local _Oxxl = _XooX - (_lIoo.phaseAt or _XooX)
            local _XxX = _XooX - (_lIoo.passAt or _XooX)
            local _xolO = _lxxl ~= nil
            if _xIlo and not _xolO and _Oxxl > _xIlo and _lIoo.reported ~= _IXIx then
                _lIoo.reported = _IXIx
                local _IIoX, _oXIX = _lXxX.humanoid(), _lXxX._oXIX()
                local _XoXo, _oIOx, _lloX = _XIXo.eggInventory()
                local _XoOo = _xolx.trustCooldown()
                _oloX.warn("WATCHDOG run %d: %s for %.1fs (limit %ds) uid=%s | humanoid=%s hp=%s root=%s anchored=%s"
                    .. " | ragdoll=%.1fs | movement owner=%s | last pickup=%s | retries=%d | inventory=%s/%s"
                    .. " | trust cooldown=%.0fs | pass started %.1fs ago",
                    _oXOo, _IXIx, _Oxxl, _xIlo, tostring(_lIoo._OXXX),
                    tostring(_IIoX ~= nil and _IIoX.Parent ~= nil), _IIoX and ("%.0f"):format(_IIoX.Health) or "-",
                    tostring(_oXIX ~= nil), tostring(_oXIX and _oXIX.Anchored),
                    _lXIo.ragdollRemaining(), tostring(_XooO._Xolo()), tostring(_lIoo._IooX),
                    _lIoo._IIlO or 0, tostring(_oIOx), tostring(_lloX), _XoOo, _XxX)
            end
            if not _xolO and _XxX > 150 then
                _oloX.error("run %d: no progress for %.0fs (phase %s) - stopping the run", _oXOo, _XxX, tostring(_IXIx))
                task.spawn(_XIlX, "stalled: no progress for " .. math.floor(_XxX) .. "s")
            end
        end)
    end
    _XIxX.onTeardown("autosteal", function()
        if _lIlO then _XIlX("hub unloaded") end
    end)
    function _xolx.setOptions(_oOXX, _XIOx)
        if type(_oOXX) == "table" or _oOXX == nil then _oOXX, _XIOx = "main", _oOXX end
        _oOXX = tostring(_oOXX)
        _oOIO[_oOXX] = _XIOx or {}
        if _lIlO and _Xolo == _oOXX then
            _Xxxo = _oOIO[_oOXX]
            _oloX._XIxo("%s updated its options mid-run", _oOXX)
        end
    end
    function _xolx.setEnabled(_IoIx, _oOXX)
        _oOXX = tostring(_oOXX or "main")
        if _IoIx then
            setAnimationsLocked(true)
            local _lOIO, _oxXX = _oOOo(_oOXX)
            if _lOIO == false then
                setAnimationsLocked(false)
                return false, _oxXX
            end
        else
            if _lIlO and _Xolo ~= nil and _Xolo ~= _oOXX then
                _oloX._XIxo("%s asked to stop, but %s owns this run - ignored", _oOXX, _Xolo)
                return false
            end
            _XIlX("toggled off")
            setAnimationsLocked(false)
        end
        return true
    end
    function _xolx._Xolo() return _Xolo end
    function _xolx.isRunning()
        return _lIlO
    end
    function _xolx.runOnce(cancelFn)
        local _XlOO = snapshot()
        local _xOIx, _oxXX, _IlIo = runCycle(_oxol, cancelFn or function() return false end)
        local _oOxO = snapshot()
        if _IlIo then reportCycle(_xOIx, _oxXX, _IlIo, _XlOO, _oOxO) end
        return _xOIx, _oxXX, _IlIo, _XlOO, _oOxO
    end
    function _xolx._IXXO()
        return {
            _lIlO  = _lIlO,
            _oXOo    = _oxol,
            _OXOO   = _OXOO,
            _xxOl = _xxOl,
            _oIxo     = _lIlO and _lxxl or nil,
            tier     = _OOOX.tier,
            scope    = _lIlx and _lIlx:_IXOO() or nil,
        }
    end
    _xolx._XIlX = _XIlX
    return _xolx
end)
_XIxX.module("features.bossfight", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _OOOX  = _XIxX.require("core.device")
    local _lXxX   = _XIxX.require("core.character")
    local _OooX  = _XIxX.require("core.net")
    local _Oxoo = _XIxX.require("features.boss")
    local _xOoX  = _XIxX.require("features.movement")
    local _Oooo = _XIxX.require("features.autosteal")
    local _XooO = _XIxX.require("core.motion")
    local _oloX  = _XIxX.require("boot.log").for_module("bossfight")
    local _xolx = {}
    local _oolx = {
        TICK            = 0.12,
        SWING_GAP       = 0.65,
        REACH           = 9,
        EQUIP_SETTLE    = 0.25,
        RESPAWN_SETTLE  = 0.6,
        HAND_REACH_Y    = 30,
        HAND_CHASE_Y    = 90,
        HAND_RISE_EPS   = 2,      -- upward studs per tick = "this arm is retracting"
        HAND_COMMIT     = 1.5,    -- seconds we stay on a chosen hand
        SURFACE_MARGIN  = -20,
        STEP_SPEED      = 420,
        MAX_STEP        = 14,
        MAX_DT          = 0.05,
        SINK_MAX        = 6,      -- below the last real floor = fell through
        Y_TAU           = 0.12,   -- seconds to close ~63% of a height change
        STUCK_TIME      = 2.5,
        RIM_SWEEP       = { 25, 50, 75, 100, 125, 150 },
        RIM_LOOKAHEAD   = 6,
        MOVE_ARRIVE     = 1.5,
        SWING_SLACK     = 4,      -- must exceed MOVE_ARRIVE or they deadlock
        AIM_COS         = 0.906,  -- cos 25 deg
        AIM_EASE        = 0.35,
        TRACK_TAU       = 0.18,   -- low-pass on a hand's jittering position
        TRACK_JUMP      = 60,
        WAIT_MAX        = 2.5,    -- longest we hold for a hazard to clear
        FLING_UP        = 60,
        FLING_MULT      = 2.0,
        GROUND_BAND     = 25,
        PROBE_UP        = 40,
        PROBE_DOWN      = 220,
        SOLID_STEPS     = 8,
        IGNORE_TTL      = 0.5,    -- the raycast ignore list is rebuilt this often
        RING_STEP_DEG   = 22,
        RING_RADII      = { 1.0, 0.85, 1.15, 0.7, 1.3 },
        AROUND_ANGLES   = { 25, 45, 70, 95, 120, 145 },
        AROUND_FRAC     = 0.55,
        AROUND_MIN_R    = 90,
        HAZARD_CACHE    = 0.1,
        HAZARD_CLEAR    = 6,
        SLAM_CLEAR      = 12,
        RING_CLEAR      = 2,      -- the red rings are 2 studs wide, not walls
        HOLE_CLEAR      = 6,
        DODGE_GAP       = 0.08,
        DODGE_POINTS    = 16,
        DODGE           = false,  -- V3.1 BX.bossDodgeEnabled. Shipped off.
        ORBIT_TRIGGER   = 34,
        ORBIT_STEP      = 0.55,
        VOID_GAP        = 0.2,
        VOID_MISSES     = 3,
        VOID_DROP_PROOF = 25,
        MAX_RISE        = 8,
        HAND_BONES      = { "UpperHand1.R", "UpperHand1.L", "LowerHand1.R", "LowerHand1.L" },
        WALK            = true,
        WALK_LOOKAHEAD  = 24,
        SNAP_GAP        = 8,
        SNAPS           = 3,
        SNAP_WINDOW     = 4,
        BACKOFF_FIRST   = 1,
        BACKOFF_MAX     = 8,
        SKIP_AFTER      = 4,
        SKIP_STUCK      = 3,
        SKIP_FOR        = 15,
        LEAVE_GAP       = 3,
        LEAVE_TRIES     = 5,
        TOWERS_TTL      = 2,      -- the crystal Hitbox list is re-walked this often
    }
    _xolx._oolx = _oolx
    local _lIlx, _olxl = nil, false
    local _xOOo = { swings = 0, dodges = 0, flings = 0, voidSaves = 0, rescues = 0, kills = 0 }
    function _xolx._xOOo() return table._OIIo(_xOOo) end
    function _xolx.isOn() return _olxl end
    local _lXlx = nil
    local function _XoIo()
        return {
            _xoXo = nil, dodge = nil, _xxlX = nil, trackPos = nil,
            handY = {}, handPick = nil, handPickAt = 0,
            lastSolid = nil, arenaFloorY = nil,
            stuckBest = nil, stuckSince = nil, stuckFlip = false, rimSide = 1,
            lastSwingAt = 0, batFor = nil, waitAt = nil, idlePhase = false,
            arena = nil, hazards = nil, hazardsAt = 0,
            _OloO = nil, ignoreAt = 0,
            inArena = false, noclipped = false, _IOxo = false,
            settleUntil = 0, batAskedAt = 0,
            voidAnchor = nil, voidMisses = 0,
            lastLog = {},
            phase = nil, _Xlxo = nil,
            wrote = nil, snaps = {}, holdUntil = 0, backoff = 0, backoffs = 0,
            sidesteps = 0, skip = {}, goalKey = nil,
            killClaimed = false, leaveTries = 0, leaveAt = 0,
            _OxXO = nil, towersAt = 0,
            _IOOo = nil,
        }
    end
    local function trail(_IOOo, _XXOO)
        if not _lXlx or _lXlx._IOOo == _IOOo then return end
        _lXlx._IOOo = _IOOo
        _oloX._XIxo("fight: %s%s", _IOOo, _XXOO and (" (" .. tostring(_XXOO) .. ")") or "")
    end
    local function every(_xIoX, _OxIX, _XoOX, ...)
        local _XooX = _loIx.clock()
        if _XooX - (_lXlx.lastLog[_xIoX] or 0) < _OxIX then return end
        _lXlx.lastLog[_xIoX] = _XooX
        _oloX._XIxo(_XoOX, ...)
    end
    local function inArena()
        return _OoXX.LocalPlayer:GetAttribute("InBossArena") == true
    end
    _xolx.inArena = inArena
    local function arena()
        local _oXlx = _lXlx.arena
        if _oXlx and _oXlx.Parent then return _oXlx end
        _oXlx = workspace:FindFirstChild("BossArena") or workspace:FindFirstChild("BossArena", true)
        _lXlx.arena = _oXlx
        return _oXlx
    end
    local function arenaFloor()
        local _oXlx = arena()
        local _Oxlx = _oXlx and _oXlx:FindFirstChild("Floor", true)
        if _Oxlx and _Oxlx:IsA("BasePart") then return _Oxlx end
        return nil
    end
    local function arenaCentre()
        local _Oxlx = arenaFloor()
        if _Oxlx then return _Oxlx.Position end
        local _oXlx = arena()
        if _oXlx and _oXlx.PrimaryPart then return _oXlx.PrimaryPart.Position end
        return nil
    end
    local function bossModel()
        local _oXlx = arena()
        if not _oXlx then return nil end
        local _XXlx = _oXlx:FindFirstChild("Boss", true)
        if _XXlx and _XXlx:IsA("Model") then return _XXlx end
        return nil
    end
    local function phase()
        local _XXlx = bossModel()
        if not _XXlx then return nil end
        if _XXlx:GetAttribute("Spawning") then return nil end
        if _XXlx:GetAttribute("PhaseTwoAt") ~= nil then return "hands" end
        return "crystals"
    end
    local _OIo = RaycastParams._oooX()
    _OIo.FilterType = Enum.RaycastFilterType.Exclude
    _OIo.IgnoreWater = true
    local function refreshIgnore()
        local _XooX = _loIx.clock()
        if _lXlx._OloO and (_XooX - _lXlx.ignoreAt) < _oolx.IGNORE_TTL then return end
        local _OloO = {}
        for _OXlx, pl in ipairs(_OoXX.Players:GetPlayers()) do
            if pl.Character then _OloO[#_OloO + 1] = pl.Character end
        end
        local _oXlx = arena()
        if _oXlx then
            for _OXlx, nm in ipairs({ "CrystalTowers", "Boss", "SlamIndicator",
                                  "SlamArmHitbox", "SlamRestHitbox" }) do
                local _Ixlx = _oXlx:FindFirstChild(nm, true)
                if _Ixlx then _OloO[#_OloO + 1] = _Ixlx end
            end
        end
        for _OXlx, nm in ipairs({ "BossHazards", "BossBlackHole" }) do
            local _Ixlx = workspace:FindFirstChild(nm)
            if _Ixlx then _OloO[#_OloO + 1] = _Ixlx end
        end
        _OIo.FilterDescendantsInstances = _OloO
        _lXlx._OloO, _lXlx.ignoreAt = _OloO, _XooX
    end
    local function groundAt(_IIXX)
        refreshIgnore()
        local _IXXX = _IIXX.Y + _oolx.PROBE_UP
        local _Oxlx = arenaFloor()
        if _Oxlx then _IXXX = math._IOoX(_IXXX, _Oxlx.Position.Y + _oolx.PROBE_UP) end
        local _oxlo = math._IOoX(_oolx.PROBE_DOWN, (_IXXX - _IIXX.Y) + _oolx.PROBE_DOWN)
        local _IlOx = workspace:Raycast(Vector3._oooX(_IIXX.X, _IXXX, _IIXX.Z),
                                    Vector3._oooX(0, -_oxlo, 0), _OIo)
        if not _IlOx then return nil end
        if _Oxlx and (_IlOx.Position.Y - _Oxlx.Position.Y) > _oolx.GROUND_BAND then return nil end
        return _IlOx.Position.Y
    end
    local function onFloor(_IIXX) return groundAt(_IIXX) ~= nil end
    local function lastSolidToward(_ooXo, _Xllx)
        local _IoXo = Vector3._oooX(_Xllx.X - _ooXo.X, 0, _Xllx.Z - _ooXo.Z)
        local _xlXo = _IoXo.Magnitude
        if _xlXo < 1 then return nil end
        local _oOOX = _IoXo.Unit
        local _oXoo
        local _oIlX = math._IOoX(_xlXo / _oolx.SOLID_STEPS, 20)
        for _xxlx = 1, _oolx.SOLID_STEPS do
            local _Ixlx = _oIlX * _xxlx
            if _Ixlx > _xlXo then break end
            local _xIOx = _ooXo + _oOOX * _Ixlx
            local _IIIx = groundAt(Vector3._oooX(_xIOx.X, _ooXo.Y, _xIOx.Z))
            if not _IIIx then break end
            _oXoo = Vector3._oooX(_xIOx.X, _IIIx, _xIOx.Z)
        end
        return _oXoo
    end
    local function clearLine(_oXlx, _XXlx)
        local _IoXo = Vector3._oooX(_XXlx.X - _oXlx.X, 0, _XXlx.Z - _oXlx.Z)
        local _xlXo = _IoXo.Magnitude
        if _xlXo < 1 then return true end
        local _oOOX = _IoXo.Unit
        local _oIlX = math._IOoX(_xlXo / _oolx.SOLID_STEPS, 20)
        for _xxlx = 1, _oolx.SOLID_STEPS do
            local _Ixlx = _oIlX * _xxlx
            if _Ixlx >= _xlXo then break end
            local _xIOx = _oXlx + _oOOX * _Ixlx
            if not groundAt(Vector3._oooX(_xIOx.X, _oXlx.Y, _xIOx.Z)) then return false end
        end
        return true
    end
    local function ringWaypoint(_ooXo, _Xllx)
        local _oOoX = arenaCentre()
        if not _oOoX then return nil end
        local _oXlx = Vector3._oooX(_ooXo.X - _oOoX.X, 0, _ooXo.Z - _oOoX.Z)
        local _XXlx = Vector3._oooX(_Xllx.X - _oOoX.X, 0, _Xllx.Z - _oOoX.Z)
        if _oXlx.Magnitude < 20 or _XXlx.Magnitude < 20 then return nil end
        local _oOoo, _XOoo = math.atan2(_oXlx.Z, _oXlx.X), math.atan2(_XXlx.Z, _XXlx.X)
        local _XlXo = _XOoo - _oOoo
        while _XlXo > math.pi do _XlXo = _XlXo - 2 * math.pi end
        while _XlXo < -math.pi do _XlXo = _XlXo + 2 * math.pi end
        local _oIlX = math.min(math.abs(_XlXo), math.rad(_oolx.RING_STEP_DEG))
        if _XlXo < 0 then _oIlX = -_oIlX end
        local _oolX = _oOoo + _oIlX
        for _OXlx, mul in ipairs(_oolx.RING_RADII) do
            local _IlOx = _oXlx.Magnitude * mul
            local _xIOx = Vector3._oooX(_oOoX.X + math.cos(_oolX) * _IlOx, _ooXo.Y, _oOoX.Z + math.sin(_oolX) * _IlOx)
            local _IIIx = groundAt(_xIOx)
            if _IIIx then
                local _oOlx = Vector3._oooX(_xIOx.X, _IIIx, _xIOx.Z)
                if clearLine(_ooXo, _oOlx) then return _oOlx, math.deg(_oIlX) end
            end
        end
        return nil
    end
    local function rotated(_oOOX, _oXlx)
        return Vector3._oooX(_oOOX.X * math.cos(_oXlx) - _oOOX.Z * math.sin(_oXlx), 0,
                           _oOOX.X * math.sin(_oXlx) + _oOOX.Z * math.cos(_oXlx))
    end
    local function detourAround(_ooXo, _Xllx)
        if clearLine(_ooXo, _Xllx) then return nil end
        local _IoXo = Vector3._oooX(_Xllx.X - _ooXo.X, 0, _Xllx.Z - _ooXo.Z)
        local _xlXo = _IoXo.Magnitude
        if _xlXo < 1 then return nil end
        local _oOOX = _IoXo.Unit
        local _IlOx = math._IOoX(_xlXo * _oolx.AROUND_FRAC, _oolx.AROUND_MIN_R)
        for _OXlx, deg in ipairs(_oolx.AROUND_ANGLES) do
            for _OXlx, sign in ipairs({ 1, -1 }) do
                local _oOlx = _ooXo + rotated(_oOOX, math.rad(deg) * sign) * _IlOx
                local _IIIx = groundAt(Vector3._oooX(_oOlx.X, _ooXo.Y, _oOlx.Z))
                if _IIIx then
                    _oOlx = Vector3._oooX(_oOlx.X, _IIIx, _oOlx.Z)
                    if clearLine(_ooXo, _oOlx) and clearLine(_oOlx, _Xllx) then return _oOlx, deg * sign end
                end
            end
        end
        for _OXlx, deg in ipairs(_oolx.AROUND_ANGLES) do
            for _OXlx, sign in ipairs({ 1, -1 }) do
                local _oOlx = _ooXo + rotated(_oOOX, math.rad(deg) * sign) * _IlOx
                local _IIIx = groundAt(Vector3._oooX(_oOlx.X, _ooXo.Y, _oOlx.Z))
                if _IIIx and clearLine(_ooXo, Vector3._oooX(_oOlx.X, _IIIx, _oOlx.Z)) then
                    return Vector3._oooX(_oOlx.X, _IIIx, _oOlx.Z), deg * sign
                end
            end
        end
        return nil
    end
    local function hazardParts()
        local _XooX = _loIx.clock()
        if _lXlx.hazards and (_XooX - _lXlx.hazardsAt) < _oolx.HAZARD_CACHE then return _lXlx.hazards end
        local _lxoX = {}
        local _IIoO = workspace:FindFirstChild("BossHazards")
        if _IIoO then
            for _OXlx, _Ixlx in ipairs(_IIoO:GetDescendants()) do
                if _Ixlx:IsA("BasePart") then _lxoX[#_lxoX + 1] = _Ixlx end
            end
        end
        local _oXlx = arena()
        if _oXlx then
            for _OXlx, _oXxo in ipairs({ "SlamIndicator", "SlamArmHitbox", "SlamRestHitbox" }) do
                local _Ixlx = _oXlx:FindFirstChild(_oXxo)
                if _Ixlx and _Ixlx:IsA("BasePart") then _lxoX[#_lxoX + 1] = _Ixlx end
            end
        end
        local _loxX = workspace:FindFirstChild("BossBlackHole")
        if _loxX and _loxX:IsA("BasePart") then _lxoX[#_lxoX + 1] = _loxX end
        _lXlx.hazards, _lXlx.hazardsAt = _lxoX, _XooX
        return _lxoX
    end
    local function hazardClear(_XIIX)
        local _oIOx = _XIIX.Name
        if _oIOx == "BossBlackHole" then return _oolx.HOLE_CLEAR end
        if _oIOx:find("Slam") then return _oolx.SLAM_CLEAR end
        if _oIOx:find("Ring") then return _oolx.RING_CLEAR end
        return _oolx.HAZARD_CLEAR
    end
    local function inHazard(_XIIX, _IIXX, _IOIo)
        local _lIIo = hazardClear(_XIIX) + (_IOIo or 0)
        if _XIIX:IsA("Part") and _XIIX.Shape == Enum.PartType.Cylinder then
            local _IoXo = Vector3._oooX(_IIXX.X - _XIIX.Position.X, 0, _IIXX.Z - _XIIX.Position.Z)
            return _IoXo.Magnitude <= _XIIX.Size.Y * 0.5 + _lIIo
        end
        local _xIXX = _XIIX.CFrame:PointToObjectSpace(_IIXX)
        local _XXXo = _XIIX.Size * 0.5
        return math.abs(_xIXX.X) <= _XXXo.X + _lIIo
            and math.abs(_xIXX.Z) <= _XXXo.Z + _lIIo
            and math.abs(_xIXX.Y) <= _XXXo.Y + 8
    end
    local function inAnyHazard(_IIXX, _IOIo)
        if not _oolx.DODGE then return nil end
        for _OXlx, _XIIX in ipairs(hazardParts()) do
            if inHazard(_XIIX, _IIXX, _IOIo) then return _XIIX end
        end
        return nil
    end
    local function dodgeScore(_OIlX, _OxXo)
        local _xxlX = _lXlx._xxlX
        if typeof(_xxlX) == "Vector3" then
            return Vector3._oooX(_OIlX.X - _xxlX.X, 0, _OIlX.Z - _xxlX.Z).Magnitude
        end
        return Vector3._oooX(_OIlX.X - _OxXo.X, 0, _OIlX.Z - _OxXo.Z).Magnitude
    end
    local function dodgeHazards()
        if not _oolx.DODGE then _lXlx.dodge = nil return false end
        local _Xxlx = _lXxX._oXIX()
        if not _Xxlx then return false end
        local _lXlo = hazardParts()
        if #_lXlo == 0 then _lXlx.dodge = nil return false end
        local _lxOX = nil
        for _OXlx, _XIIX in ipairs(_lXlo) do
            if inHazard(_XIIX, _Xxlx.Position) then _lxOX = _XIIX break end
        end
        if not _lxOX then _lXlx.dodge = nil return false end
        local _OxXo = _Xxlx.Position
        local _lxxO = {}
        if _lxOX:IsA("Part") and _lxOX.Shape == Enum.PartType.Cylinder then
            local _oolX = _lxOX.Size.Y * 0.5 + _oolx.HOLE_CLEAR + 4
            for _xxlx = 0, _oolx.DODGE_POINTS - 1 do
                local _IIOX = (2 * math.pi / _oolx.DODGE_POINTS) * _xxlx
                _lxxO[#_lxxO + 1] = Vector3._oooX(_lxOX.Position.X + math.cos(_IIOX) * _oolX, _OxXo.Y,
                                                _lxOX.Position.Z + math.sin(_IIOX) * _oolX)
            end
        else
            local _xIXX = _lxOX.CFrame:PointToObjectSpace(_OxXo)
            local _XXXo = _lxOX.Size * 0.5
            local _lIIo = hazardClear(_lxOX) + 4
            local _IIIX = (_xIXX.X >= 0 and 1 or -1) * (_XXXo.X + _lIIo)
            local _lIIX = (_xIXX.Z >= 0 and 1 or -1) * (_XXXo.Z + _lIIo)
            local _IXxX = _lxOX.CFrame
            _lxxO[#_lxxO + 1] = _IXxX:PointToWorldSpace(Vector3._oooX(_xIXX.X, _xIXX.Y, _lIIX))
            _lxxO[#_lxxO + 1] = _IXxX:PointToWorldSpace(Vector3._oooX(_IIIX, _xIXX.Y, _xIXX.Z))
            _lxxO[#_lxxO + 1] = _IXxX:PointToWorldSpace(Vector3._oooX(_xIXX.X, _xIXX.Y, -_lIIX))
            _lxxO[#_lxxO + 1] = _IXxX:PointToWorldSpace(Vector3._oooX(-_IIIX, _xIXX.Y, _xIXX.Z))
            _lxxO[#_lxxO + 1] = _IXxX:PointToWorldSpace(Vector3._oooX(_IIIX, _xIXX.Y, _lIIX))
            _lxxO[#_lxxO + 1] = _IXxX:PointToWorldSpace(Vector3._oooX(-_IIIX, _xIXX.Y, _lIIX))
        end
        local _oXoo, _oXx
        for _OXlx, _OIlX in ipairs(_lxxO) do
            if onFloor(_OIlX) and not inAnyHazard(_OIlX, 0) then
                local _XlXX = dodgeScore(_OIlX, _OxXo)
                if not _oXx or _XlXX < _oXx then _oXoo, _oXx = _OIlX, _XlXX end
            end
        end
        if not _oXoo then
            for _OXlx, _OIlX in ipairs(_lxxO) do
                if onFloor(_OIlX) then
                    local _XlXX = dodgeScore(_OIlX, _OxXo)
                    if not _oXx or _XlXX < _oXx then _oXoo, _oXx = _OIlX, _XlXX end
                end
            end
        end
        if not _oXoo then
            local _oOoX = arenaCentre()
            if _oOoX then
                local _xloO = Vector3._oooX(_oOoX.X - _OxXo.X, 0, _oOoX.Z - _OxXo.Z)
                if _xloO.Magnitude > 1 then
                    _oXoo = _OxXo + _xloO.Unit * math.min(_xloO.Magnitude, 60)
                end
            end
        end
        if not _oXoo then return true end
        _lXlx.dodge = { _IIXX = _oXoo }
        _xOOo.dodges = _xOOo.dodges + 1
        return true
    end
    local function orbitPoint(_oOlX, _oxlo)
        local _Xxlx = _lXxX._oXIX()
        local _loxX = workspace:FindFirstChild("BossBlackHole")
        if not _Xxlx or not _loxX or not _loxX:IsA("BasePart") then return nil end
        local _IxXO = Vector3._oooX(_loxX.Position.X - _Xxlx.Position.X, 0, _loxX.Position.Z - _Xxlx.Position.Z)
        if _IxXO.Magnitude > _oolx.ORBIT_TRIGGER then return nil end
        local _xIXX = Vector3._oooX(_Xxlx.Position.X - _oOlX.X, 0, _Xxlx.Position.Z - _oOlX.Z)
        if _xIXX.Magnitude < 1 then _xIXX = Vector3._oooX(1, 0, 0) end
        local _IIOX = math.atan2(_xIXX.Z, _xIXX.X)
        local _IlOx = math._IOoX(_oxlo, 6)
        local function _oOxX(_oXlx)
            return Vector3._oooX(_oOlX.X + math.cos(_oXlx) * _IlOx, _Xxlx.Position.Y, _oOlX.Z + math.sin(_oXlx) * _IlOx)
        end
        local _ooIx, _XoIx = _oOxX(_IIOX + _oolx.ORBIT_STEP), _oOxX(_IIOX - _oolx.ORBIT_STEP)
        local function fromHole(_xIOx)
            return Vector3._oooX(_xIOx.X - _loxX.Position.X, 0, _xIOx.Z - _loxX.Position.Z).Magnitude
        end
        local _xOIo, _XOXO = _ooIx, _XoIx
        if fromHole(_XoIx) > fromHole(_ooIx) then _xOIo, _XOXO = _XoIx, _ooIx end
        if onFloor(_xOIo) then return _xOIo end
        if onFloor(_XOXO) then return _XOXO end
        return nil
    end
    local function isBatTool(_OlOx)
        return _OlOx:IsA("Tool") and (_OlOx:GetAttribute("IsBat") == true or _OlOx.Name:find("Bat") ~= nil)
    end
    local function equipBat()
        local _xxoo = _lXxX.get()
        if not _xxoo then return nil end
        for _OXlx, _OlOx in ipairs(_xxoo:GetChildren()) do
            if isBatTool(_OlOx) then return _OlOx end
        end
        local _OoxX = _OoXX.LocalPlayer:FindFirstChild("Backpack")
        if _OoxX then
            for _OXlx, _OlOx in ipairs(_OoxX:GetChildren()) do
                if isBatTool(_OlOx) then
                    local _IIoX = _lXxX.humanoid()
                    local _xOIx = _IIoX and pcall(function() _IIoX:EquipTool(_OlOx) end)
                    if not _xOIx or _OlOx.Parent ~= _xxoo then _OlOx.Parent = _xxoo end
                    _oloX._XIxo("equipped %s", _OlOx.Name)
                    return _OlOx
                end
            end
        end
        return nil
    end
    local _olOO, _Xol, _Ixo = 0, nil, nil
    local function batSwing(_oIOX)
        local _xOIx = pcall(function()
            local _IlXX = _OooX.find("RE/BatSwing/Trigger")
            assert(_IlXX, "no BatSwing remote")
            _olOO = _olOO + 1
            _IlXX:FireServer(nil, ("%d:%d:%d"):format(_OoXX.LocalPlayer.UserId, _olOO,
                math.floor(workspace:GetServerTimeNow() * 1000)))
        end)
        if not _xOIx then
            pcall(function() _oIOX:Activate() end)
            return
        end
        pcall(function()
            local _xOoo = _oIOX:FindFirstChild("HitAnim")
            local _IIoX = _lXxX.humanoid()
            local _OlOl = _IIoX and _IIoX:FindFirstChildOfClass("Animator")
            if _xOoo and _OlOl then
                if _Ixo ~= _OlOl then
                    _Xol = _OlOl:LoadAnimation(_xOoo)
                    _Ixo = _OlOl
                end
                _Xol:Play()
            end
            local _OOXX = _oIOX:FindFirstChild("Slash", true)
            if _OOXX and _OOXX:IsA("Sound") then _OOXX:Play() end
        end)
    end
    local function readyAfterRagdoll()
        local _oIIx, _Xxlx = _lXxX.humanoid(), _lXxX._oXIX()
        if not _oIIx or not _Xxlx then return end
        _oIIx.PlatformStand = false
        _oIIx.Sit = false
        _oIIx.AutoRotate = true
        local _xIlx = _oIIx:GetState()
        if _xIlx == Enum.HumanoidStateType.Physics
           or _xIlx == Enum.HumanoidStateType.PlatformStanding
           or _xIlx == Enum.HumanoidStateType.FallingDown
           or _xIlx == Enum.HumanoidStateType.Ragdoll
           or _xIlx == Enum.HumanoidStateType.Seated then
            _oIIx:ChangeState(Enum.HumanoidStateType.GettingUp)
        end
        _Xxlx.AssemblyLinearVelocity = Vector3.zero
        _Xxlx.AssemblyAngularVelocity = Vector3.zero
    end
    local function antiFling()
        local _Xxlx, _IIoX = _lXxX._oXIX(), _lXxX.humanoid()
        if not _Xxlx or not _IIoX then return end
        local _XlOx = _Xxlx.AssemblyLinearVelocity
        local _IoXo = (_XlOx * Vector3._oooX(1, 0, 1)).Magnitude
        local _OlOX = math._IOoX((_IIoX.WalkSpeed or 16) * _oolx.FLING_MULT, 120)
        if _XlOx.Y <= _oolx.FLING_UP and _IoXo <= _OlOX then return end
        local _llxo = Vector3.zero
        if _IoXo > 0.001 then
            _llxo = (_XlOx * Vector3._oooX(1, 0, 1)).Unit * math.min(_IoXo, _IIoX.WalkSpeed or 16)
        end
        _Xxlx.AssemblyLinearVelocity = Vector3._oooX(_llxo.X, math.min(_XlOx.Y, 0), _llxo.Z)
        _Xxlx.AssemblyAngularVelocity = Vector3.zero
        _xOOo.flings = _xOOo.flings + 1
        every("fling", 2, "cancelled a launch (up %.0f, flat %.0f) - %d so far",
            _XlOx.Y, _IoXo, _xOOo.flings)
    end
    local function targetReach(_XIIX)
        if typeof(_XIIX) == "Vector3" then return _oolx.REACH end
        if not (_XIIX and _XIIX:IsA("BasePart")) then return _oolx.REACH end
        local _XXXo = math._IOoX(_XIIX.Size.X, _XIIX.Size.Z) * 0.5
        return math._IOoX(_oolx.REACH, _XXXo + _oolx.SURFACE_MARGIN)
    end
    local function _xXXO()
        local _Xxlx = _lXxX._oXIX()
        if not _Xxlx then return nil end
        local _IXIx = phase()
        if not _IXIx then return nil end
        if _IXIx == "crystals" then
            local _XooX = _loIx.clock()
            if not _lXlx._OxXO or (_XooX - _lXlx.towersAt) > _oolx.TOWERS_TTL then
                local _oXlx = arena()
                local _OxXO = _oXlx and _oXlx:FindFirstChild("CrystalTowers", true)
                local _OOxo = {}
                if _OxXO then
                    for _OXlx, _Ixlx in ipairs(_OxXO:GetDescendants()) do
                        if _Ixlx:IsA("BasePart") and _Ixlx.Name == "Hitbox" then _OOxo[#_OOxo + 1] = _Ixlx end
                    end
                end
                _lXlx._OxXO, _lXlx.towersAt = _OOxo, _XooX
            end
            local _oXoo, _lXxO, _OllO = nil, nil, nil
            for _OXlx, _Ixlx in ipairs(_lXlx._OxXO) do
                if _Ixlx.Parent then
                    local _XIIx = _Ixlx:GetAttribute("Health")
                    if type(_XIIx) == "number" and _XIIx > 0 then
                        if (_lXlx.skip[_Ixlx] or 0) > _XooX then
                            _OllO = _Ixlx
                        else
                            local _xlXo = (_Ixlx.Position - _Xxlx.Position).Magnitude
                            if not _lXxO or _xlXo < _lXxO then _oXoo, _lXxO = _Ixlx, _xlXo end
                        end
                    end
                end
            end
            _oXoo = _oXoo or _OllO
            if _oXoo then return _oXoo, "crystal" end
            return nil
        end
        local _XXlx = bossModel()
        if not _XXlx then return nil end
        local _looX = _Xxlx.Position.Y
        local _XloX, _xOxo, _lIOX, _Iooo, _loxO
        for _OXlx, bn in ipairs(_oolx.HAND_BONES) do
            local _lxoo = _XXlx:FindFirstChild(bn, true)
            if _lxoo and _lxoo:IsA("Bone") then
                local _IIXX
                pcall(function() _IIXX = _lxoo.TransformedWorldCFrame.Position end)
                _IIXX = _IIXX or _lxoo.WorldPosition
                if _IIXX then
                    local _oOIX = _lXlx.handY[bn]
                    _lXlx.handY[bn] = _IIXX.Y
                    local _xlXO = _oOIX ~= nil and (_IIXX.Y - _oOIX) > _oolx.HAND_RISE_EPS
                    if not _xlXO then
                        local _IoXo = Vector3._oooX(_IIXX.X - _Xxlx.Position.X, 0, _IIXX.Z - _Xxlx.Position.Z).Magnitude
                        if not _Iooo or _IoXo < _Iooo then _lIOX, _Iooo, _loxO = _IIXX, _IoXo, _IIXX.Y - _looX end
                        if (_IIXX.Y - _looX) <= _oolx.HAND_REACH_Y and (not _xOxo or _IoXo < _xOxo) then
                            _XloX, _xOxo = _IIXX, _IoXo
                        end
                    end
                end
            end
        end
        local function landable(_xIOx)
            if not _xIOx then return nil end
            if onFloor(_xIOx) and clearLine(_Xxlx.Position, _xIOx) then return _xIOx end
            local _oOlx, _IIOX = ringWaypoint(_Xxlx.Position, _xIOx)
            if not _oOlx then _oOlx, _IIOX = detourAround(_Xxlx.Position, _xIOx) end
            if _oOlx then
                every("pit", 2, "pit in the way - walking round the ring (%+.0f deg)", _IIOX or 0)
                return _oOlx
            end
            return lastSolidToward(_Xxlx.Position, _xIOx)
        end
        _XloX = landable(_XloX)
        if _lIOX and (_loxO or 0) <= _oolx.HAND_CHASE_Y then _lIOX = landable(_lIOX) else _lIOX = nil end
        local _XooX = _loIx.clock()
        if _lXlx.handPick and (_XooX - _lXlx.handPickAt) < _oolx.HAND_COMMIT then
            local _llxo = _lXlx.handPick
            if (_XloX and (_XloX - _llxo).Magnitude < 220) or (_lIOX and (_lIOX - _llxo).Magnitude < 220) then
                return _llxo, "hand"
            end
        end
        if _XloX then
            _lXlx.handPick, _lXlx.handPickAt = _XloX, _XooX
            return _XloX, "hand"
        end
        if _lIOX then
            _lXlx.handPick, _lXlx.handPickAt = _lIOX, _XooX
            return _lIOX, "hand"
        end
        if _loxO then
            every("high", 2, "hands up: nearest is %.0f studs up (need <= %d) - holding for the slam",
                _loxO, _oolx.HAND_REACH_Y)
        end
        return nil
    end
    local function leaveArena()
        local _oXlx = arena()
        local _XOXo = _oXlx and _oXlx:FindFirstChild("BossArenaLeaveTeleport", true)
        local _XIIX = _XOXo and (_XOXo:IsA("BasePart") and _XOXo
            or _XOXo:FindFirstChild("Hitbox", true)
            or _XOXo:FindFirstChildWhichIsA("BasePart", true))
        local _xXlx = _lXxX.get()
        if not (_XIIX and _xXlx) then return false end
        _xXlx:MoveTo(_XIIX.Position + Vector3._oooX(0, 3, 0))
        return true
    end
    local function setNoclip(_IoIx)
        if _IoIx == _lXlx.noclipped then return end
        _lXlx.noclipped = _IoIx
        if _IoIx then
            _xOoX.noclip(true)
        elseif not _Oooo.isRunning() then
            _xOoX.noclip(false)
        end
    end
    local function skipTarget(_oxXX)
        local _xIoX = _lXlx.goalKey
        if typeof(_xIoX) == "Instance" then
            _lXlx.skip[_xIoX] = _loIx.clock() + _oolx.SKIP_FOR
            _oloX.warn("fight: NEXT TARGET - skipping this crystal for %ds (%s)", _oolx.SKIP_FOR, _oxXX)
        else
            _lXlx.holdUntil = math._IOoX(_lXlx.holdUntil, _loIx.clock() + _oolx.SKIP_FOR / 3)
            _oloX.warn("fight: holding %ds before chasing the hands again (%s)", math.floor(_oolx.SKIP_FOR / 3), _oxXX)
        end
        _lXlx._xoXo, _lXlx.goalKey, _lXlx.backoffs, _lXlx.sidesteps, _lXlx.backoff = nil, nil, 0, 0, 0
    end
    local function noteSnap(_Xlxo)
        if not _lXlx or not _lXlx.inArena then return end
        local _XooX = _loIx.clock()
        for _xxlx = #_lXlx.snaps, 1, -1 do
            if _XooX - _lXlx.snaps[_xxlx] > _oolx.SNAP_WINDOW then table.remove(_lXlx.snaps, _xxlx) end
        end
        _lXlx.snaps[#_lXlx.snaps + 1] = _XooX
        if #_lXlx.snaps < _oolx.SNAPS then return end
        _lXlx.snaps = {}
        _lXlx.backoff = math.min(_lXlx.backoff > 0 and _lXlx.backoff * 2 or _oolx.BACKOFF_FIRST, _oolx.BACKOFF_MAX)
        _lXlx.backoffs = _lXlx.backoffs + 1
        _lXlx.holdUntil = _XooX + _lXlx.backoff
        _lXlx._xoXo, _lXlx.wrote = nil, nil
        _xOOo.snapBackoffs = (_xOOo.snapBackoffs or 0) + 1
        _oloX.warn("fight: movement interrupted (%s x%d in %ds) - holding %.0fs (backoff %d/%d)",
            tostring(_Xlxo), _oolx.SNAPS, _oolx.SNAP_WINDOW, _lXlx.backoff, _lXlx.backoffs, _oolx.SKIP_AFTER)
        readyAfterRagdoll()
        if _lXlx.backoffs >= _oolx.SKIP_AFTER then skipTarget("server kept moving us back") end
    end
    local function moverStep(_xXxX)
        if not _lXlx.inArena or _Oooo.isRunning() or _XooO._XXx("bossfight") then return end
        if _lXlx.settleUntil and _loIx.clock() < _lXlx.settleUntil then return end
        if _loIx.clock() < _lXlx.holdUntil then return end
        do
            local _OIIx, _OxOX = _lXxX._oXIX(), _lXxX.humanoid()
            if _OIIx and _lXlx.wrote and (_loIx.clock() - (_lXlx.wroteAt or 0)) < 0.2 then
                if (_OIIx.Position - _lXlx.wrote).Magnitude > _oolx.SNAP_GAP then
                    _lXlx.wrote = nil
                    noteSnap("snap")
                    return
                end
            end
            if _OIIx and _lXlx.walking and _lXlx._oIIO then
                local _Olll = math._IOoX((_OxOX and _OxOX.WalkSpeed or 16) * math.min(_xXxX, 0.1) * 3, 25)
                if (_OIIx.Position - _lXlx._oIIO).Magnitude > _Olll then
                    _lXlx._oIIO = _OIIx.Position
                    noteSnap("walk snap")
                    return
                end
            end
            _lXlx._oIIO = _OIIx and _OIIx.Position or nil
        end
        antiFling()
        local _Ilxl = _lXlx.dodge ~= nil
        local _xoXo = _lXlx.dodge or _lXlx._xoXo
        local _Xxlx, _IIoX = _lXxX._oXIX(), _lXxX.humanoid()
        if not _xoXo then
            if _lXlx.walking and _Xxlx and _IIoX then _IIoX:MoveTo(_Xxlx.Position) _lXlx.walking = false end
            return
        end
        if not _Xxlx or not _IIoX then return end
        if groundAt(_Xxlx.Position) then
            _lXlx.lastSolid = _Xxlx.Position
        elseif _lXlx.lastSolid then
            local _oooo = Vector3._oooX(_lXlx.lastSolid.X - _Xxlx.Position.X, 0, _lXlx.lastSolid.Z - _Xxlx.Position.Z)
            if _oooo.Magnitude > 1 then
                local _xOXX = math.min(_oooo.Magnitude, math.min(_xXxX, _oolx.MAX_DT) * _oolx.STEP_SPEED, _oolx.MAX_STEP)
                local _XOIx = _Xxlx.Position + _oooo.Unit * _xOXX
                local _XXOX = groundAt(_XOIx) or _lXlx.lastSolid.Y
                _IIoX.PlatformStand = false
                _Xxlx.CFrame = CFrame.lookAt(Vector3._oooX(_XOIx.X, _XXOX, _XOIx.Z), Vector3._oooX(_XOIx.X, _XXOX, _XOIx.Z) + _oooo.Unit)
                _lXlx.wrote, _lXlx.wroteAt = Vector3._oooX(_XOIx.X, _XXOX, _XOIx.Z), _loIx.clock()
                _Xxlx.AssemblyLinearVelocity = Vector3.zero
                _xOOo.rescues = _xOOo.rescues + 1
                every("rescue", 1, "no ground underneath - walking back to solid")
            end
            return
        end
        local _IoXo = Vector3._oooX(_xoXo._IIXX.X - _Xxlx.Position.X, 0, _xoXo._IIXX.Z - _Xxlx.Position.Z)
        local _oxlo = _Ilxl and 0 or (_xoXo._oxlo or _oolx.REACH)
        local _IOxo = _IoXo.Magnitude - _oxlo
        if _IOxo <= _oolx.MOVE_ARRIVE then
            if _Ilxl then _lXlx.dodge = nil else _lXlx._xoXo = nil end
            _lXlx.backoff, _lXlx.backoffs, _lXlx.sidesteps = 0, 0, 0
            trail("ARRIVED")
            return
        end
        local _XooX = _loIx.clock()
        if not _lXlx.stuckBest or _IOxo < _lXlx.stuckBest - 2 then _lXlx.stuckBest, _lXlx.stuckSince = _IOxo, _XooX end
        local _xXOO = _IoXo.Unit
        if _lXlx.stuckSince and (_XooX - _lXlx.stuckSince) > _oolx.STUCK_TIME then
            _lXlx.stuckFlip = not _lXlx.stuckFlip
            local _IOXX = _lXlx.stuckFlip and 1 or -1
            _xXOO = Vector3._oooX(-_IoXo.Unit.Z * _IOXX, 0, _IoXo.Unit.X * _IOXX)
            _lXlx.stuckSince, _lXlx.stuckBest = _XooX, nil
            _lXlx.sidesteps = _lXlx.sidesteps + 1
            every("stuck", 2, "not making progress - sidestepping (%d/%d)", _lXlx.sidesteps, _oolx.SKIP_STUCK)
            if _lXlx.sidesteps >= _oolx.SKIP_STUCK then
                skipTarget("no progress after " .. _lXlx.sidesteps .. " sidesteps")
                return
            end
        end
        local _oIlX = math.min(_IOxo, math.min(_xXxX, _oolx.MAX_DT) * _oolx.STEP_SPEED, _oolx.MAX_STEP)
        local _xooX = _Xxlx.Position + _xXOO * _oIlX
        if not _Ilxl and inAnyHazard(_xooX, 0) then return end
        local function groundFor(_oOOX, _xlXo)
            local _lxlo = _Xxlx.Position + _oOOX * _xlXo
            return groundAt(Vector3._oooX(_lxlo.X, _Xxlx.Position.Y, _lxlo.Z))
        end
        local _IIIx = groundFor(_xXOO, _oIlX)
        if _IIIx then
            _lXlx.arenaFloorY = _IIIx
        elseif _lXlx.arenaFloorY and _Xxlx.Position.Y < _lXlx.arenaFloorY - _oolx.SINK_MAX then
            _Xxlx.CFrame = CFrame._oooX(_Xxlx.Position.X, _lXlx.arenaFloorY, _Xxlx.Position.Z)
            _lXlx.wrote, _lXlx.wroteAt = Vector3._oooX(_Xxlx.Position.X, _lXlx.arenaFloorY, _Xxlx.Position.Z), _loIx.clock()
            _Xxlx.AssemblyLinearVelocity = Vector3.zero
            every("sink", 2, "dropped below the floor - lifted back onto it")
            return
        end
        if not _IIIx then
            local _OoIo = nil
            for _OXlx, deg in ipairs(_oolx.RIM_SWEEP) do
                for _OXlx, _IOXX in ipairs(_lXlx.rimSide == -1 and { -1, 1 } or { 1, -1 }) do
                    local _Ixlx = rotated(_xXOO, math.rad(deg * _IOXX))
                    local _oxlx = groundFor(_Ixlx, _oIlX)
                    if _oxlx and groundFor(_Ixlx, _oIlX + _oolx.RIM_LOOKAHEAD) then
                        _OoIo, _IIIx = _Ixlx, _oxlx
                        _lXlx.rimSide = _IOXX
                        break
                    end
                end
                if _OoIo then break end
            end
            if not _OoIo then
                if _Ilxl then _lXlx.dodge = nil else _lXlx._xoXo = nil end
                return
            end
            _xXOO = _OoIo
            _xooX = _Xxlx.Position + _xXOO * _oIlX
            _lXlx.stuckSince = _XooX
            every("rim", 2, "hole in the way - following the rim round")
        end
        _IIoX.PlatformStand = false
        if _oolx.WALK then
            local _xxlX = _Xxlx.Position + _xXOO * math.min(_IOxo + 2, _oolx.WALK_LOOKAHEAD)
            _IIoX:MoveTo(Vector3._oooX(_xxlX.X, _IIIx, _xxlX.Z))
            _lXlx.walking, _lXlx.wrote, _lXlx.wroteAt = true, nil, _loIx.clock()
            return
        end
        local _oIXo = _Xxlx.Position.Y
        local _IIOx = 1 - math.exp(-_xXxX / _oolx.Y_TAU)
        local _OlXo = Vector3._oooX(_xooX.X, _oIXo + (_IIIx - _oIXo) * _IIOx, _xooX.Z)
        _IIoX:Move(Vector3.zero, false)
        _Xxlx.CFrame = CFrame.lookAt(_OlXo, _OlXo + _IoXo.Unit)
        _lXlx.wrote, _lXlx.wroteAt = _OlXo, _loIx.clock()
        _Xxlx.AssemblyLinearVelocity = Vector3._oooX(0, _Xxlx.AssemblyLinearVelocity.Y, 0)
        _Xxlx.AssemblyAngularVelocity = Vector3.zero
    end
    local function fightTick()
        local _XloO = inArena()
        if _XloO ~= _lXlx.inArena then
            _lXlx.inArena = _XloO
            setNoclip(_XloO)
            _lXlx._xoXo, _lXlx.dodge, _lXlx._xxlX, _lXlx.trackPos, _lXlx.handPick = nil, nil, nil, nil, nil
            _lXlx.lastSolid, _lXlx.arenaFloorY, _lXlx._IOxo = nil, nil, false
            _lXlx.voidAnchor, _lXlx.voidMisses = nil, 0
            _lXlx.snaps, _lXlx.holdUntil, _lXlx.backoff, _lXlx.backoffs, _lXlx.sidesteps = {}, 0, 0, 0, 0
            _lXlx.wrote, _lXlx.goalKey, _lXlx.killClaimed, _lXlx.leaveTries, _lXlx._IOOo = nil, nil, false, 0, nil
            if _XloO then
                _lXlx.settleUntil = _loIx.clock() + _oolx.RESPAWN_SETTLE
                readyAfterRagdoll()
                _XooO.claim("bossfight")
                trail("EVENT", "entered the arena")
            else
                _XooO.release("bossfight")
            end
            _oloX._XIxo(_XloO and "in the arena - fighting" or "left the arena")
        end
        if not _XloO or _Oooo.isRunning() then return end
        if _lXlx.settleUntil and _loIx.clock() < _lXlx.settleUntil then return end
        local _oIOX = equipBat()
        if not _oIOX then
            if _loIx.clock() - (_lXlx.batAskedAt or 0) > 5 then
                _lXlx.batAskedAt = _loIx.clock()
                local _xXoX, _IXxo = _OooX.call("RF/Codex/AskWearFieldBat")
                _oloX._XIxo("no bat - AskWearFieldBat -> %s %s", tostring(_xXoX), tostring(_IXxo or ""))
            end
        elseif _lXlx.batFor ~= _oIOX then
            _lXlx.batFor = _oIOX
            task.wait(_oolx.EQUIP_SETTLE)
        end
        local _oxOX = _lXxX.humanoid()
        if _oxOX then
            local _IoXX = _oxOX:GetState()
            if _oxOX.PlatformStand or _IoXX == Enum.HumanoidStateType.Physics
               or _IoXX == Enum.HumanoidStateType.PlatformStanding
               or _IoXX == Enum.HumanoidStateType.None then
                readyAfterRagdoll()
            end
        end
        local _IxIo = dodgeHazards()
        local _IIlX = _Oxoo.snapshot()
        local _xIXo = _IIlX and tonumber(_IIlX.BossHealth) and _IIlX.BossHealth <= 0
        if _xIXo then
            _lXlx._xoXo, _lXlx._xxlX = nil, nil
            if not _lXlx.killClaimed then
                _lXlx.killClaimed = true
                _xOOo.kills = _xOOo.kills + 1
                trail("BOSS UPDATE", "boss dead")
                local _oIOx = _Oxoo.claimMilestones()
                _oloX._XIxo("boss dead - claimed %d milestone(s)", _oIOx)
            end
            local _XooX = _loIx.clock()
            if _lXlx.leaveTries < _oolx.LEAVE_TRIES and (_XooX - _lXlx.leaveAt) >= _oolx.LEAVE_GAP then
                _lXlx.leaveTries, _lXlx.leaveAt = _lXlx.leaveTries + 1, _XooX
                _lXlx.wrote = nil
                local _IOIO = leaveArena()
                _oloX._XIxo("walking out of the arena (try %d/%d) -> %s", _lXlx.leaveTries, _oolx.LEAVE_TRIES, tostring(_IOIO))
            elseif _lXlx.leaveTries >= _oolx.LEAVE_TRIES then
                every("leavefail", 15, "boss dead but still in the arena after %d walk-outs - holding", _lXlx.leaveTries)
            end
            _lXlx._IOxo = true
            return
        elseif _lXlx._IOxo then
            _lXlx._IOxo, _lXlx.killClaimed, _lXlx.leaveTries = false, false, 0
        end
        local _Oool = phase()
        if _Oool ~= _lXlx.phase then
            trail(_lXlx.phase == nil and "BOSS FOUND" or "BOSS UPDATE", "phase " .. tostring(_Oool or "spawning"))
        end
        _lXlx.phase = _Oool
        if _loIx.clock() < _lXlx.holdUntil then return end
        local _XIIX, _Xlxo = _xXXO()
        if _XIIX ~= nil and (typeof(_XIIX) == "Instance" and _XIIX or "hand") ~= _lXlx.goalKey then
            _lXlx.goalKey = (typeof(_XIIX) == "Instance") and _XIIX or "hand"
            _lXlx.backoff, _lXlx.backoffs, _lXlx.sidesteps = 0, 0, 0
            trail("NEXT TARGET", tostring(_Xlxo))
        end
        if not _XIIX then
            _lXlx._xoXo, _lXlx._xxlX, _lXlx._Xlxo = nil, nil, nil
            if _lXlx.idlePhase ~= _lXlx.phase then
                _lXlx.idlePhase = _lXlx.phase
                _oloX._XIxo("nothing to hit (phase=%s) - holding position", tostring(_lXlx.phase or "spawning"))
            end
            return
        end
        _lXlx.idlePhase, _lXlx._Xlxo = false, _Xlxo
        local _oOlX = (typeof(_XIIX) == "Vector3") and _XIIX or _XIIX.Position
        local _Xxlx = _lXxX._oXIX()
        if not _Xxlx then return end
        local _oxlo = targetReach(_XIIX)
        local _xOxl = Vector3._oooX(_oOlX.X - _Xxlx.Position.X, 0, _oOlX.Z - _Xxlx.Position.Z)
        local _Ixlx = _xOxl.Magnitude
        local _OOOo = _Xxlx.Position + (_Ixlx > 0.001 and _xOxl.Unit * math._IOoX(_Ixlx - _oxlo, 0) or Vector3.zero)
        if inAnyHazard(Vector3._oooX(_OOOo.X, _Xxlx.Position.Y, _OOOo.Z), 0) then
            _lXlx.waitAt = _lXlx.waitAt or _loIx.clock()
            if _loIx.clock() - _lXlx.waitAt < _oolx.WAIT_MAX then
                _lXlx._xoXo = nil
                return
            end
        else
            _lXlx.waitAt = nil
        end
        _lXlx._xxlX = _oOlX
        if _Ixlx > _oxlo + _oolx.SWING_SLACK then
            local _IoXO = _oOlX
            if _Xlxo == "hand" then
                local _oOIX = _lXlx.trackPos
                if _oOIX and (_oOIX - _oOlX).Magnitude < _oolx.TRACK_JUMP then
                    _IoXO = _oOIX:Lerp(_oOlX, 1 - math.exp(-_oolx.TICK / _oolx.TRACK_TAU))
                end
                _lXlx.trackPos = _IoXO
            else
                _lXlx.trackPos = nil
            end
            _lXlx._xoXo = { _IIXX = _IoXO, _oxlo = _oxlo }
            trail("MOVING", tostring(_Xlxo))
            return
        end
        local _lolo = orbitPoint(_oOlX, _oxlo)
        if _lolo then
            _lXlx._xoXo = { _IIXX = _lolo, _oxlo = 0 }
            every("orbit", 3, "black hole is on us - orbiting the target")
        else
            _lXlx._xoXo = nil
        end
        if _IxIo then return end
        local _IoXo = Vector3._oooX(_oOlX.X - _Xxlx.Position.X, 0, _oOlX.Z - _Xxlx.Position.Z)
        if _IoXo.Magnitude > 0.1 then
            local _IXlO = _IoXo.Unit
            local _XXxl = _Xxlx.CFrame.LookVector * Vector3._oooX(1, 0, 1)
            _XXxl = _XXxl.Magnitude > 0.001 and _XXxl.Unit or _IXlO
            if _XXxl:Dot(_IXlO) < _oolx.AIM_COS then
                local _IOOX = _Xxlx.CFrame
                _Xxlx.CFrame = _IOOX:Lerp(CFrame.lookAt(_IOOX.Position, _IOOX.Position + _IXlO), _oolx.AIM_EASE)
            end
        end
        if not _oIOX or not _oIOX.Parent then return end
        if _oIOX:GetAttribute("CooldownActive") == true then return end
        if _loIx.clock() - _lXlx.lastSwingAt < _oolx.SWING_GAP then return end
        _lXlx.lastSwingAt = _loIx.clock()
        batSwing(_oIOX)
        _xOOo.swings = _xOOo.swings + 1
        trail("ATTACKING", tostring(_Xlxo))
        _lXlx.backoff, _lXlx.backoffs, _lXlx.sidesteps = 0, 0, 0
        if _xOOo.swings % 20 == 1 then
            _oloX._XIxo("swinging at the %s (%d swings)", tostring(_Xlxo), _xOOo.swings)
        end
    end
    local function voidTick()
        if not _lXlx.inArena then return end
        local _xXlx, _Xxlx = _lXxX.get(), _lXxX._oXIX()
        if not (_xXlx and _Xxlx) then return end
        local _IIXX = _Xxlx.Position
        local _IIIx = groundAt(_IIXX)
        if _IIIx and math.abs(_IIXX.Y - _IIIx) <= _oolx.MAX_RISE then
            _lXlx.voidAnchor = Vector3._oooX(_IIXX.X, _IIIx, _IIXX.Z)
            _lXlx.voidMisses = 0
            return
        end
        if not _IIIx then _lXlx.voidMisses = _lXlx.voidMisses + 1 else _lXlx.voidMisses = 0 end
        local _oOxl = _lXlx.voidAnchor and (_IIXX.Y < _lXlx.voidAnchor.Y - _oolx.VOID_DROP_PROOF)
        if _lXlx.voidMisses >= _oolx.VOID_MISSES and _oOxl then
            _lXlx.voidMisses = 0
            local _oooo = _lXlx.voidAnchor or arenaCentre()
            if _oooo then
                _xOOo.voidSaves = _xOOo.voidSaves + 1
                _Xxlx.AssemblyLinearVelocity = Vector3.zero
                _Xxlx.AssemblyAngularVelocity = Vector3.zero
                _xXlx:MoveTo(_oooo)
                _Xxlx.CFrame = CFrame._oooX(_oooo)
                _lXlx.wrote, _lXlx.wroteAt = _oooo, _loIx.clock()
                _oloX._XIxo("voidwatch: off the floor at (%.0f, %.0f, %.0f) - pulled back (#%d)",
                    _IIXX.X, _IIXX.Y, _IIXX.Z, _xOOo.voidSaves)
                task.wait(0.3)
            end
        end
    end
    function _xolx._IXXO()
        if not _olxl then return { _OXOo = "Auto fight", _Ixoo = "off" } end
        if _Oooo.isRunning() then
            return { _OXOo = "Auto fight", _Ixoo = "ON  \u{B7}  waiting for Auto Steal to finish" }
        end
        if not _lXlx.inArena then
            local _lxXo = _Oxoo._lxXo()
            if _lxXo and _lxXo.Open == true then
                return { _OXOo = "Auto fight", _Ixoo = _Oxoo.autoEnterOn()
                    and "ON  \u{B7}  boss open - entering"
                    or "ON  \u{B7}  boss open - press Enter or turn on Auto enter" }
            end
            return { _OXOo = "Auto fight", _Ixoo = "ON  \u{B7}  waiting for the boss world to open" }
        end
        if _lXlx._IOxo then return { _OXOo = "Auto fight", _Ixoo = "Boss dead  \u{B7}  leaving" } end
        local _IXIx = _lXlx.phase
        if not _IXIx then return { _OXOo = "Auto fight", _Ixoo = "In the arena  \u{B7}  boss spawning" } end
        local _XolX = _lXlx._Xlxo and ("hitting the " .. _lXlx._Xlxo) or "holding"
        return { _OXOo = "Auto fight",
                 _Ixoo = ("Fighting  \u{B7}  %s  \u{B7}  %s  \u{B7}  %d swings"):format(_IXIx, _XolX, _xOOo.swings) }
    end
    function _xolx.setEnabled(_IoIx)
        _IoIx = _IoIx and true or false
        if _IoIx == _olxl then return true end
        if not _IoIx then
            _olxl = false
            _XooO.release("bossfight")
            if _lIlx then _lIlx:destroy() _lIlx = nil end
            if _lXlx then
                _lXlx._xoXo, _lXlx.dodge, _lXlx._xxlX = nil, nil, nil
                setNoclip(false)
                _XIxX.try("bossfight.offRestore", readyAfterRagdoll)
            end
            _lXlx = nil
            _oloX._XIxo("off (%d swings, %d kills this session)", _xOOo.swings, _xOOo.kills)
            return true
        end
        if not _Oxoo.isOn() then _Oxoo.setEnabled(true) end
        _lXlx = _XoIo()
        _lIlx = _XIxX.scope("features.bossfight")
        _olxl = true
        _lIlx:onFrame("mover", _OoXX.RunService.Heartbeat, moverStep)
        _lIlx:loop("fight", _oolx.TICK, fightTick)
        _lIlx:loop("void", _oolx.VOID_GAP, voidTick)
        if _oolx.DODGE then
            _lIlx:loop("dodge", _oolx.DODGE_GAP, function()
                if _lXlx.inArena then dodgeHazards() end
            end)
        end
        _lXxX.onSpawn(_lIlx, "bossfight.respawn", function()
            if not _lXlx then return end
            setNoclip(false)
            _lXlx._xoXo, _lXlx.dodge, _lXlx._xxlX, _lXlx.trackPos, _lXlx.batFor = nil, nil, nil, nil, nil
            _lXlx.lastSolid, _lXlx.arenaFloorY, _lXlx._IOxo = nil, nil, false
            _lXlx.voidAnchor, _lXlx.voidMisses = nil, 0
            _lXlx.inArena, _lXlx.noclipped = false, false
            _lXlx.snaps, _lXlx.holdUntil, _lXlx.backoff, _lXlx.backoffs, _lXlx.sidesteps = {}, 0, 0, 0, 0
            _lXlx.wrote, _lXlx.goalKey, _lXlx._IOOo = nil, nil, nil
            _XooO.release("bossfight")     -- re-claimed on the arena edge
            _lXlx.settleUntil = _loIx.clock() + _oolx.RESPAWN_SETTLE
        end)
        _XooO.onRejected(_lIlx, function(_Xlxo)
            if _lXlx and _lXlx.inArena and _lXlx.wroteAt and (_loIx.clock() - _lXlx.wroteAt) < 0.5 then noteSnap(_Xlxo) end
        end)
        _oloX._XIxo("on (tick %.2fs, swing %.2fs, dodge %s) - waiting for the arena",
            _oolx.TICK, _oolx.SWING_GAP, _oolx.DODGE and "on" or "off")
        return true
    end
    _XIxX.onTeardown("bossfight", function() _xolx.setEnabled(false) end)
    return _xolx
end)
_XIxX.module("features.prewarm", function(_XIxX)
    local _OoXX  = _XIxX.require("core.services")
    local _oloX  = _XIxX.require("boot.log").for_module("prewarm")
    local _xolx = {}
    local _lIlx = nil
    local _IoOo = {}      -- { name, ms, detail }
    local _IOXo = false
    function _xolx.report() return table._OIIo(_IoOo) end
    function _xolx.isDone() return _IOXo end
    local function record(_oXxo, _oOIx, _XXOO)
        _IoOo[#_IoOo + 1] = { _oXxo = _oXxo, _oOIx = _oOIx, _XXOO = _XXOO }
    end
    function _xolx._oOOo()
        if _lIlx then return false end
        _lIlx = _XIxX.scope("features.prewarm")
        _lIlx:spawn("warm", function()
            local _Ollx = _loIx.clock()
            local _lXXo = _XIxX.require("features.grab")
            _OoXX.RunService.Heartbeat:Wait()
            _XIxX.try("prewarm.prompts", function()
                local _oOIx, _oIOx = _lXXo.warmPrompts()
                record("prompts", _oOIx, _oIOx .. " prompts")
            end)
            local _lOIX = _XIxX.require("features.plot")
            _OoXX.RunService.Heartbeat:Wait()
            _XIxX.try("prewarm.safeZone", function()
                local _IIlx = _loIx.clock()
                local _OXlx, _xXXX = _lOIX.safeZone()
                record("safeZone", (_loIx.clock() - _IIlx) * 1000, tostring(_xXXX))
            end)
            _OoXX.RunService.Heartbeat:Wait()
            _XIxX.try("prewarm.plotHome", function()
                local _IIlx = _loIx.clock()
                local _OXlx, _xXXX = _lOIX._XxXo()
                record("plotHome", (_loIx.clock() - _IIlx) * 1000, tostring(_xXXX))
            end)
            local _Xooo = _XIxX.require("features.bait")
            _OoXX.RunService.Heartbeat:Wait()
            _XIxX.try("prewarm.baitArea", function()
                local _IIlx = _loIx.clock()
                local _looo = _Xooo.firstAreaId(6)
                record("baitArea", (_loIx.clock() - _IIlx) * 1000, tostring(_looo))
            end)
            local _xoxo = _XIxX.require("features.movement")
            local _lXxX = _XIxX.require("core.character")
            _OoXX.RunService.Heartbeat:Wait()
            _XIxX.try("prewarm.ground", function()
                local _XxOX = _lXxX._oXIX()
                if not _XxOX then record("ground", 0, "no character") return end
                local _IIlx = _loIx.clock()
                local _lOOx = _xoxo.groundY(_XxOX.Position)
                record("ground", (_loIx.clock() - _IIlx) * 1000,
                    _lOOx and ("y=" .. ("%.0f"):format(_lOOx)) or "no hit")
            end)
            _IOXo = true
            local _lXlo = {}
            local _XXOo = 0
            for _OXlx, _llOx in ipairs(_IoOo) do
                _lXlo[#_lXlo + 1] = ("%s=%.1fms(%s)"):format(_llOx._oXxo, _llOx._oOIx, _llOx._XXOO)
                _XXOo = _XXOo + _llOx._oOIx
            end
            _oloX._XIxo("prewarmed in %.0fms wall, %.1fms of work: %s",
                (_loIx.clock() - _Ollx) * 1000, _XXOo, table.concat(_lXlo, " "))
        end)
        return true
    end
    function _xolx._XIlX()
        if not _lIlx then return end
        _lIlx:destroy()
        _lIlx = nil
    end
    return _xolx
end)
_XIxX.module("features.targetline", function(_XIxX)
    local _OoXX = _XIxX.require("core.services")
    local _lXxX = _XIxX.require("core.character")
    local _OOXo = _XIxX.require("features.eggs")
    local _lOIX = _XIxX.require("features.plot")
    local _xolx = {}
    local _lIlx, _OXoo, _OoIx, _ooIx, _XlxX, _xlxX
    local _olo, _xlll = nil, false
    local function cleanup()
        if _lIlx then pcall(function() _lIlx:destroy() end) _lIlx = nil end
        for _OXlx, _IOOx in ipairs({_OXoo,_OoIx,_ooIx}) do if _IOOx then pcall(function() _IOOx:Destroy() end) end end
        _OXoo,_OoIx,_ooIx,_XlxX,_xlxX=nil,nil,nil,nil,nil
    end
    local function makePoint(_oXxo)
        local _xIOx=Instance._oooX("Part")
        _xIOx.Name=_oXxo; _xIOx.Size=Vector3._oooX(.2,.2,.2); _xIOx.Anchored=true
        _xIOx.CanCollide=false; _xIOx.CanTouch=false; _xIOx.CanQuery=false; _xIOx.Transparency=1; _xIOx.Parent=workspace
        local _oXlx=Instance._oooX("Attachment"); _oXlx.Parent=_xIOx
        return _xIOx,_oXlx
    end
    local function ensure()
        if _OXoo and _OXoo.Parent then return end
        _OoIx,_XlxX=makePoint("RyuzakiLineStart"); _ooIx,_xlxX=makePoint("RyuzakiLineEnd")
        _OXoo=Instance._oooX("Beam"); _OXoo.Name="RyuzakiSelectedEggLine"
        _OXoo.Attachment0=_XlxX; _OXoo.Attachment1=_xlxX; _OXoo.FaceCamera=true
        _OXoo.Color=ColorSequence._oooX(Color3.fromRGB(255,0,0)); _OXoo.Width0=.12; _OXoo.Width1=.12
        _OXoo.LightEmission=1; _OXoo.Transparency=NumberSequence._oooX(.05); _OXoo.Parent=_OoIx
    end
    function _xolx.setSelected(_OXXX) _olo=_OXXX; _xlll=false; ensure() end
    function _xolx.setReturning(_IoIx) _xlll=_IoIx and true or false; ensure() end
    function _xolx._lIIo() _olo=nil; _xlll=false; cleanup() end
    local function update()
        if not _olo then return end
        ensure()
        local _oXIX=_lXxX._oXIX()
        if not _oXIX then _OXoo.Enabled=false; return end
        local _OlXo
        if _xlll then _OlXo=select(1,_lOIX.safeZone()) else local _lxlx=_OOXo.get(_olo); _OlXo=_lxlx and _lxlx._IIXX end
        if not _OlXo then _OXoo.Enabled=false; return end
        _OoIx.CFrame=CFrame._oooX(_oXIX.Position); _ooIx.CFrame=CFrame._oooX(_OlXo); _OXoo.Enabled=true
    end
    function _xolx._oOOo()
        if _lIlx then return end
        _lIlx=_XIxX.scope("features.targetline")
        _lIlx:onFrame("update",_OoXX.RunService.Heartbeat,update)
    end
    _xolx._oOOo()
    _XIxX.onTeardown("targetline",cleanup)
    return _xolx
end)
do
    local _OooO = _XIxX.require("boot.log")
    _OooO._XIlo = _XIxX.require("core.config").LOG_LEVEL
    local _oloX = _OooO.for_module("startup")
    _OooO.session(("RyuzakiHub %s build %s | generation %d")
        :format(_XIxX.version, _XIxX._XXxO, _XIxX.generation))
    local _xllO = { _XOOo = "BOOTING", _XoXO = {}, _Ollx = _loIx.clock() }
    local _IoOX = (type(getgenv) == "function" and getgenv()) or _G
    _IoOX.RyuzakiStartup = _xllO
    local function setState(_llOx)
        _xllO._XOOo = _llOx
        _oloX._XIxo("state -> %s", _llOx)
    end
    local function record(_oXxo, _olXO, _XXOO, _oOIx)
        _xllO._XoXO[#_xllO._XoXO + 1] = {
            _oXxo = _oXxo, _olXO = _olXO, _XXOO = _XXOO,
            _oOxX = _loIx.clock() - _xllO._Ollx, _oOIx = _oOIx,
        }
        local _lOxo = ("stage %-14s %6.0fms  %s%s"):format(_oXxo, _oOIx or 0, _olXO,
            _XXOO and (": " .. tostring(_XXOO)) or "")
        if _olXO == "FAILED" then _oloX.error("%s", _lOxo)
        elseif _olXO == "FALLBACK" then _oloX.warn("%s", _lOxo)
        else _oloX._XIxo("%s", _lOxo) end
    end
    local function _IOOo(_oXxo, _xXol, _xxxX)
        local _IIlx = _loIx.clock()
        local _xOIx, _OlXX = pcall(_xxxX)
        local _oOIx = (_loIx.clock() - _IIlx) * 1000
        if _xOIx then
            record(_oXxo, _OlXX == "FALLBACK" and "FALLBACK" or "OK",
                type(_OlXX) == "string" and _OlXX ~= "FALLBACK" and _OlXX or nil, _oOIx)
            return true, _OlXX
        end
        record(_oXxo, "FAILED", _OlXX, _oOIx)
        if _xXol then
            _xllO.failedAt = _oXxo
            _xllO.error = tostring(_OlXX)
        end
        return false, _OlXX
    end
    setState("BOOTING")
    if not _IOOo("services", true, function()
        _XIxX.require("core.services")
    end) then
        warn("[RYUZAKI] startup failed at services: " .. tostring(_xllO.error))
        warn("[RYUZAKI] see RyuzakiHub_trace.txt")
        return
    end
    _IOOo("exec", false, function() _XIxX.require("core.exec") end)
    _IOOo("device", false, function() _XIxX.require("core.device") end)
    _IOOo("state", false, function() _XIxX.require("core.state") end)
    _IOOo("util", false, function() _XIxX.require("core.util") end)
    _IOOo("character", false, function() _XIxX.require("core.character") end)
    setState("LOADING")
    local _ooXO = {
        _oIlX = function() end, discord = function() end,
        fail = function() end, _IOXo = function() end,
        isWaitingForUser = function() return false end,
        whenClosed = function(_xxxX) pcall(_xxxX) end,
    }
    _ooXO._oIlX("Checking your game", 0.25)
    _IOOo("eggs", false, function()
        local _OOXo = _XIxX.require("features.eggs")
        if not _OOXo._Xxlo then return "FALLBACK" end
    end)
    setState("UI_BUILDING")
    _ooXO._oIlX("Loading interface", 0.45)
    local _XxXX
    _IOOo("direct ui", false, function()
        _XxXX = _XIxX.require("ui.window")
        if not _XxXX._xOIx then return "FALLBACK" end
    end)
    _IOOo("hide menu", false, function()
        if _XxXX and _XxXX._xOIx and type(_XxXX.hide) == "function" then
            if not _XxXX.hide() then return "FALLBACK" end
        end
    end)
    local _OxX
    local function buildRyuzakiPanel()
        if _OxX and _OxX.Parent then
            _OxX:Destroy()
        end
        local Players = game:GetService("Players")
        local _oxlX = game:GetService("UserInputService")
        local TweenService = game:GetService("TweenService")
        local _XxO = Players.LocalPlayer
        local _xXoO = game:GetService("CoreGui")
        pcall(function()
            if type(_oOXo) == "table" and _oOXo.hiddenParent then
                _xXoO = _oOXo.hiddenParent()
            end
        end)
        if not _xXoO then _xXoO = _XxO:WaitForChild("PlayerGui") end
        local _OOXo = _XIxX.require("features.eggs")
        local _XIXo = _XIxX.require("core.data")
        local _Oooo = _XIxX.require("features.autosteal")
        local _oIx = _XIxX.require("features.targetline")
        _OxX = Instance._oooX("ScreenGui")
        _OxX.Name = "RYUZAKI_HUB_ARCADE"
        _OxX.ResetOnSpawn = false
        _OxX.IgnoreGuiInset = true
        _OxX.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
        _OxX.Parent = _xXoO
        local _IXlo = Instance._oooX("Frame")
        _IXlo.Name = "RYUZAKI_HUB"
        _IXlo.Size = UDim2.fromOffset(195, 275)
        _IXlo.Position = UDim2.fromOffset(62, 70)
        _IXlo.BackgroundColor3 = Color3.fromRGB(70, 5, 22)
        _IXlo.BorderSizePixel = 0
        _IXlo.Active = true
        _IXlo.Parent = _OxX
        local _xoIx = Instance._oooX("UICorner", _IXlo)
        _xoIx.CornerRadius = UDim._oooX(0, 10)
        local _lXIx = Instance._oooX("UIStroke", _IXlo)
        _lXIx.Color = Color3.fromRGB(180, 25, 55)
        _lXIx.Thickness = 2
        _lXIx.Transparency = 0.08
        local _lOOO = Instance._oooX("TextButton")
        _lOOO.Name = "RYUZAKI_BUBBLE"
        _lOOO.Size = UDim2.fromOffset(44, 44)
        _lOOO.Position = UDim2.fromOffset(10, 76)
        _lOOO.BackgroundColor3 = Color3.fromRGB(70, 5, 22)
        _lOOO.BorderSizePixel = 0
        _lOOO.Text = "R"
        _lOOO.AutoButtonColor = false
        _lOOO.ZIndex = 20
        _lOOO.Parent = _OxX
        local _XOO = Instance._oooX("ImageLabel")
        _XOO.Name = "BubbleImage"
        _XOO.Size = UDim2._oooX(1, -6, 1, -6)
        _XOO.Position = UDim2.fromOffset(3, 3)
        _XOO.BackgroundTransparency = 1
        _XOO.Image = "rbxthumb://type=Asset&id=121722228686565&w=420&h=420"
        _XOO.ScaleType = Enum.ScaleType.Crop
        _XOO.ZIndex = 21
        _XOO.Parent = _lOOO
        local _Ol = Instance._oooX("UICorner", _XOO)
        _Ol.CornerRadius = UDim._oooX(1, 0)
        local _IoxX = Instance._oooX("UICorner", _lOOO)
        _IoxX.CornerRadius = UDim._oooX(1, 0)
        local _XoxX = Instance._oooX("UIStroke", _lOOO)
        _XoxX.Color = Color3.fromRGB(180, 25, 55)
        _XoxX.Thickness = 2
        _XoxX.Transparency = 0.05
        local _lxo = true
        _IXlo.Position = UDim2.fromOffset(0, 76)
        local _xOO = Instance._oooX("UIScale")
        _xOO.Scale = 1
        _xOO.Parent = _lOOO

        local function bubbleClickEffect()
            local _lOXo = TweenService:Create(
                _xOO,
                TweenInfo._oooX(0.08, Enum.EasingStyle.Quad, Enum.EasingDirection.Out),
                {Scale = 0.86}
            )
            local _IOlx = TweenService:Create(
                _xOO,
                TweenInfo._oooX(0.14, Enum.EasingStyle.Back, Enum.EasingDirection.Out),
                {Scale = 1}
            )
            _lOXo:Play()
            _lOXo.Completed:Connect(function()
                if _xOO.Parent then _IOlx:Play() end
            end)
        end

        local function placePanelOnRightEdge()
            -- Keep the panel fixed against the right edge of the phone screen,
            -- independent of the floating bubble position.
            local _xOOO = workspace.CurrentCamera
            local _lOXl = _xOOO and _xOOO.ViewportSize or Vector2._oooX(800, 600)
            local _oooO = 10
            local _loX = _IXlo.AbsoluteSize.X > 0 and _IXlo.AbsoluteSize.X or 195
            local _IOOx = math._IOoX(_oooO, _lOXl.X - _loX - _oooO)
            local _lOOx = _lOOO.AbsolutePosition.Y - _OxX.AbsolutePosition.Y
            _IXlo.Position = UDim2.fromOffset(_IOOx, math._IOoX(_oooO, _lOOx))
        end
        placePanelOnRightEdge()


        _lOOO.MouseButton1Click:Connect(function()
            bubbleClickEffect()
            _lxo = not _lxo
            if _lxo then
                placePanelOnRightEdge()
                _IXlo.Visible = true
                _lOOO.Text = "R"
            else
                _IXlo.Visible = false
                _lOOO.Text = "R"
            end
        end)
        local _OXOo = Instance._oooX("TextLabel")
        _OXOo.Size = UDim2._oooX(0, 84, 0, 26)
        _OXOo.Position = UDim2.fromOffset(10, 3)
        _OXOo.BackgroundTransparency = 1
        _OXOo.Text = "RYUZAKI HUB"
        _OXOo.TextColor3 = Color3.fromRGB(255, 245, 245)
        _OXOo.TextSize = 13
        _OXOo.Font = Enum.Font.GothamBold
        _OXOo.TextXAlignment = Enum.TextXAlignment.Left
        _OXOo.Parent = _IXlo

        -- Lista começa minimizada. ^ abre a lista; v fecha/minimiza.
        local _lxl = false
        local _XXIl = Instance._oooX("TextButton")
        _XXIl.Name = "ListToggle"
        _XXIl.Size = UDim2.fromOffset(18, 20)
        _XXIl.Position = UDim2.fromOffset(94, 5)
        _XXIl.BackgroundTransparency = 1
        _XXIl.BorderSizePixel = 0
        _XXIl.AutoButtonColor = false
        _XXIl.Text = "^"
        _XXIl.TextColor3 = Color3.fromRGB(255, 235, 240)
        _XXIl.TextSize = 14
        _XXIl.Font = Enum.Font.GothamBold
        _XXIl.ZIndex = 5
        _XXIl.Parent = _IXlo

        local _XXXO = Instance._oooX("Frame")
        _XXXO.Size = UDim2.fromOffset(76, 20)
        _XXXO.Position = UDim2._oooX(1, -82, 0, 5)
        _XXXO.BackgroundTransparency = 1
        _XXXO.Parent = _IXlo
        local _IOIl = Instance._oooX("TextButton")
        _IOIl.Size = UDim2.fromOffset(34, 19)
        _IOIl.Position = UDim2.fromOffset(0, 0)
        _IOIl.BackgroundColor3 = Color3.fromRGB(100, 8, 30)
        _IOIl.BorderSizePixel = 0
        _IOIl.Text = "GEN"
        _IOIl.TextColor3 = Color3.fromRGB(255, 225, 230)
        _IOIl.TextSize = 7
        _IOIl.Font = Enum.Font.GothamBold
        _IOIl.AutoButtonColor = false
        _IOIl.Parent = _XXXO
        Instance._oooX("UICorner", _IOIl).CornerRadius = UDim._oooX(0, 7)
        local _Xxl = Instance._oooX("TextButton")
        _Xxl.Size = UDim2.fromOffset(40, 19)
        _Xxl.Position = UDim2.fromOffset(34, 0)
        _Xxl.BackgroundColor3 = Color3.fromRGB(48, 3, 14)
        _Xxl.BorderSizePixel = 0
        _Xxl.Text = "RARITY"
        _Xxl.TextColor3 = Color3.fromRGB(235, 205, 212)
        _Xxl.TextSize = 6
        _Xxl.Font = Enum.Font.GothamBold
        _Xxl.AutoButtonColor = false
        _Xxl.Parent = _XXXO
        Instance._oooX("UICorner", _Xxl).CornerRadius = UDim._oooX(0, 7)
        local _OOXO = Instance._oooX("ScrollingFrame")
        _OOXO.Name = "ESPList"
        _OOXO.Position = UDim2.fromOffset(5, 31)
        _OOXO.Size = UDim2._oooX(1, -10, 1, -57)
        _OOXO.BackgroundColor3 = Color3.fromRGB(47, 3, 15)
        _OOXO.BackgroundTransparency = 0.08
        _OOXO.BorderSizePixel = 0
        _OOXO.ScrollBarThickness = 2
        _OOXO.ScrollBarImageColor3 = Color3.fromRGB(185, 45, 70)
        _OOXO.CanvasSize = UDim2._oooX()
        _OOXO.AutomaticCanvasSize = Enum.AutomaticSize.None
        _OOXO.Parent = _IXlo
        Instance._oooX("UICorner", _OOXO).CornerRadius = UDim._oooX(0, 7)
        local _xOIO = Instance._oooX("UIPadding", _OOXO)
        _xOIO.PaddingTop = UDim._oooX(0, 3)
        _xOIO.PaddingBottom = UDim._oooX(0, 3)
        _xOIO.PaddingLeft = UDim._oooX(0, 3)
        _xOIO.PaddingRight = UDim._oooX(0, 3)
        local _XOoO = Instance._oooX("UIListLayout", _OOXO)
        _XOoO.Padding = UDim._oooX(0, 3)
        _XOoO.SortOrder = Enum.SortOrder.LayoutOrder
        _XOoO.HorizontalAlignment = Enum.HorizontalAlignment.Center
        local _IXXO = Instance._oooX("TextLabel")
        _IXXO.Size = UDim2._oooX(1, -120, 0, 16)
        _IXXO.Position = UDim2._oooX(0, 6, 1, -19)
        _IXXO.BackgroundTransparency = 1
        _IXXO.Text = "Select an egg"
        _IXXO.TextColor3 = Color3.fromRGB(220, 190, 198)
        _IXXO.TextSize = 7
        _IXXO.Font = Enum.Font.GothamBold
        _IXXO.TextXAlignment = Enum.TextXAlignment.Left
        _IXXO.TextTruncate = Enum.TextTruncate.AtEnd
        _IXXO.Parent = _IXlo

        local _xIol = Instance._oooX("TextButton")
        _xIol.Name = "GoButton"
        _xIol.Size = UDim2.fromOffset(50, 18)
        _xIol.Position = UDim2._oooX(1, -106, 1, -20)
        _xIol.BackgroundColor3 = Color3.fromRGB(18, 105, 45)
        _xIol.BorderSizePixel = 0
        _xIol.AutoButtonColor = false
        _xIol.Text = "GO"
        _xIol.TextStrokeTransparency = 1
        _xIol.TextColor3 = Color3.fromRGB(255, 255, 255)
        _xIol.TextSize = 8
        _xIol.Font = Enum.Font.GothamBold
        _xIol.Parent = _IXlo
        Instance._oooX("UICorner", _xIol).CornerRadius = UDim._oooX(0, 7)
        local _Ilol = Instance._oooX("UIStroke", _xIol)
        _Ilol.Color = Color3.fromRGB(65, 220, 105)
        _Ilol.Thickness = 1

        local _lIx = Instance._oooX("TextButton")
        _lIx.Name = "StopButton"
        _lIx.Size = UDim2.fromOffset(50, 18)
        _lIx.Position = UDim2._oooX(1, -54, 1, -20)
        _lIx.BackgroundColor3 = Color3.fromRGB(100, 8, 30)
        _lIx.BorderSizePixel = 0
        _lIx.AutoButtonColor = false
        _lIx.Text = "STOP"
        _lIx.TextStrokeTransparency = 1
        _lIx.TextColor3 = Color3.fromRGB(255, 255, 255)
        _lIx.TextSize = 8
        _lIx.Font = Enum.Font.GothamBold
        _lIx.Parent = _IXlo
        Instance._oooX("UICorner", _lIx).CornerRadius = UDim._oooX(0, 7)
        local _OIx = Instance._oooX("UIStroke", _lIx)
        _OIx.Color = Color3.fromRGB(190, 25, 55)
        _OIx.Thickness = 1
        local function addButtonClickEffect(_oOOO)
            local _oIOo = Instance._oooX("UIScale")
            _oIOo.Scale = 1
            _oIOo.Parent = _oOOO
            _oOOO.MouseButton1Down:Connect(function()
                TweenService:Create(_oIOo, TweenInfo._oooX(0.06, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Scale = 0.94}):Play()
            end)
            _oOOO.MouseButton1Up:Connect(function()
                TweenService:Create(_oIOo, TweenInfo._oooX(0.12, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {Scale = 1}):Play()
            end)
        end

        addButtonClickEffect(_IOIl)
        addButtonClickEffect(_Xxl)
        addButtonClickEffect(_xIol)
        addButtonClickEffect(_lIx)

        local _OoO = "GEN"
        local _olo = nil
        local _OxxO = {}
        local _xIo = false

        local function applyListMode()
            if _lxl then
                _IXlo.Size = UDim2.fromOffset(195, 275)
                _OOXO.Position = UDim2.fromOffset(5, 31)
                _OOXO.Size = UDim2._oooX(1, -10, 1, -57)
                _XXIl.Text = "v"
            else
                _IXlo.Size = UDim2.fromOffset(195, 112)
                _OOXO.Position = UDim2.fromOffset(5, 31)
                _OOXO.Size = UDim2.fromOffset(185, 52)
                _XXIl.Text = "^"
                _OOXO.CanvasPosition = Vector2.zero
            end
        end

        _XXIl.MouseButton1Click:Connect(function()
            _lxl = not _lxl
            applyListMode()
        end)
        local _lXX = {
            Common = 1, Uncommon = 2, Rare = 3, Epic = 4,
            Legendary = 5, Mythic = 6, Cosmic = 7, Divine = 8,
        }
        local function fmtRate(_oIOx)
            return _OOXo.formatRate(tonumber(_oIOx) or 0)
        end
        local function fmtKg(_oIOx)
            _oIOx = tonumber(_oIOx) or 0
            if _oIOx <= 0 then return "?" end
            return _oIOx >= 100 and ("%.0f"):format(_oIOx) or ("%.1f"):format(_oIOx)
        end
        local function assetInfo(_lxlx, _oOOX)
            local _Ixlx = _lxlx and _lxlx.assetCategory and _oOOX and _oOOX[_lxlx.assetCategory] or nil
            local _OIxo = _Ixlx and _Ixlx.Icon or nil
            if type(_OIxo) == "number" then
                _OIxo = "rbxassetid://" .. tostring(_OIxo)
            elseif type(_OIxo) ~= "string" then
                _OIxo = ""
            end
            local _lIXO = (_lxlx and _lxlx._lIXO and _lxlx._lIXO ~= "?") and tostring(_lxlx._lIXO) or nil
            if not _lIXO and _Ixlx and _Ixlx.Rarity then
                _lIXO = tostring(_Ixlx.Rarity.DisplayName or _Ixlx.Rarity._id or "?")
            end
            local _oIo = Color3.fromRGB(210, 205, 210)
            if _Ixlx and _Ixlx.Rarity and typeof(_Ixlx.Rarity.Color) == "Color3" then
                _oIo = _Ixlx.Rarity.Color
            end
            return _OIxo, _lIXO or "?", _oIo
        end
        local function destroyCards()
            for _OXlx, _xXlx in ipairs(_OxxO) do
                pcall(function() _xXlx:Destroy() end)
            end
            table._lIIo(_OxxO)
        end
        local _xXOl = _XIxX.require("features.esp.cards")
        local _oOl = math._IOoX(10000, tonumber(_xXOl._oolx.MAX_DIST) or 0)
        local _Ox = 40
        local function sortedEggs()
            local _OoXO = _OOXo._OOxo()
            local _llOX = workspace.CurrentCamera
            local _oOOX = _XIXo.assetsDir()
            if not _llOX or type(_OoXO) ~= "table" then return {}, _oOOX end
            local _OoOX = _llOX.CFrame.Position
            local _OOxo = {}
            for _OXlx, _lxlx in ipairs(_OoXO) do
                if _lxlx._IIXX and (_lxlx._IIXX - _OoOX).Magnitude <= _oOl then
                    _OOxo[#_OOxo + 1] = _lxlx
                    if #_OOxo >= _Ox then break end
                end
            end
            table._lIlX(_OOxo, function(_oXlx, _XXlx)
                if _OoO == "RARITY" then
                    local _OXlx, _lxIx = assetInfo(_oXlx, _oOOX)
                    local _OXlx, _OxIx = assetInfo(_XXlx, _oOOX)
                    local _OOxX = _lXX[_lxIx] or 0
                    local _ooxX = _lXX[_OxIx] or 0
                    if _OOxX ~= _ooxX then return _OOxX > _ooxX end
                end
                local _XOxX = tonumber(_oXlx._XxOo) or 0
                local _xoxX = tonumber(_XXlx._XxOo) or 0
                if _XOxX ~= _xoxX then return _XOxX > _xoxX end
                return tostring(_oXlx._oXxo or "") < tostring(_XXlx._oXxo or "")
            end)
            return _OOxo, _oOOX
        end
        local _Xxo = Instance._oooX("Sound")
        _Xxo.Name = "EggSelectClick"
        _Xxo.SoundId = "rbxassetid://12221967"
        _Xxo.Volume = 0.45
        _Xxo.Parent = game:GetService("SoundService")
        _XIxX.onTeardown("ryuzaki.eggSelectClick", function()
            pcall(function() _Xxo:Destroy() end)
        end)

        local function playEggClick()
            pcall(function()
                _Xxo:Stop()
                _Xxo.TimePosition = 0
                _Xxo:Play()
            end)
        end

        local function selectEgg(_lxlx, _oxoo)
            if not _lxlx or not _lxlx._OXXX then return end
            _olo = _lxlx._OXXX
            _oIx.setSelected(_olo)
            _IXXO.Text = "Selected: " .. tostring(_lxlx._oXxo or "target")
            playEggClick()
            -- Keep every egg in the normal red theme; selection no longer turns green.
            for _OXlx, other in ipairs(_OxxO) do
                local _loIx = other:FindFirstChild("CardStroke")
                if _loIx then
                    _loIx.Color = Color3.fromRGB(91, 13, 32)
                    _loIx.Thickness = 1
                    other.BackgroundColor3 = Color3.fromRGB(66, 4, 19)
                end
            end
        end

        local function goSelected()
            if not _olo then
                _IXXO.Text = "Select an egg first"
                return
            end
            _Oooo.setOptions("main", { _OXXX = _olo, continuous = true })
            _oIx.setSelected(_olo)
            _oIx.setReturning(false)
            _IXXO.Text = "Auto Steal: GO"
            task.spawn(function()
                local _xOIx, _oxXX = _Oooo.setEnabled(true, "main")
                if _xOIx == false then
                    _IXXO.Text = "Auto Steal: " .. tostring(_oxXX or "failed")
                end
            end)
        end

        _xIol.MouseButton1Click:Connect(goSelected)
        _lIx.MouseButton1Click:Connect(function()
            _Oooo.setEnabled(false, "main")
            _oIx._lIIo()
            _IXXO.Text = "Auto Steal: STOP"
        end)
        local function makeCard(_lxlx, _oOOX, _lxIo)
            local _OIxo, _lIXO, _oIo = assetInfo(_lxlx, _oOOX)
            local _oxoo = Instance._oooX("TextButton")
            _oxoo.Name = "ESP_" .. tostring(_lxIo)
            _oxoo.Size = UDim2._oooX(1, -2, 0, 46)
            _oxoo.BackgroundColor3 = Color3.fromRGB(66, 4, 19)
            _oxoo.BorderSizePixel = 0
            _oxoo.AutoButtonColor = false
            _oxoo.Text = ""
            _oxoo.LayoutOrder = _lxIo
            _oxoo.Parent = _OOXO
            Instance._oooX("UICorner", _oxoo).CornerRadius = UDim._oooX(0, 7)
            local _OXXO = Instance._oooX("UIStroke", _oxoo)
            _OXXO.Name = "CardStroke"
            _OXXO.Color = Color3.fromRGB(91, 13, 32)
            _OXXO.Thickness = 1
            _OXXO.Transparency = 0.1
            local _xXIo = Instance._oooX("ImageLabel")
            _xXIo.Size = UDim2.fromOffset(34, 34)
            _xXIo.Position = UDim2.fromOffset(4, 6)
            _xXIo.BackgroundTransparency = 1
            _xXIo.ScaleType = Enum.ScaleType.Fit
            _xXIo.Image = _OIxo
            _xXIo.Parent = _oxoo
            local _oXxo = Instance._oooX("TextLabel")
            _oXxo.Size = UDim2._oooX(1, -46, 0, 13)
            _oXxo.Position = UDim2.fromOffset(43, 2)
            _oXxo.BackgroundTransparency = 1
            _oXxo.Text = tostring(_lxlx._oXxo or "Unknown")
            _oXxo.TextColor3 = Color3.fromRGB(255, 247, 247)
            _oXxo.TextSize = 9
            _oXxo.Font = Enum.Font.GothamBold
            _oXxo.TextXAlignment = Enum.TextXAlignment.Left
            _oXxo.TextTruncate = Enum.TextTruncate.AtEnd
            _oXxo.Parent = _oxoo
            local _lOxo = Instance._oooX("TextLabel")
            _lOxo.Size = UDim2._oooX(1, -46, 0, 12)
            _lOxo.Position = UDim2.fromOffset(43, 15)
            _lOxo.BackgroundTransparency = 1
            _lOxo.Text = ("Gen: %s    KG: %s"):format(fmtRate(_lxlx._XxOo), fmtKg(_lxlx._XlIx))
            _lOxo.TextColor3 = Color3.fromRGB(255, 235, 239)
            _lOxo.TextSize = 7
            _lOxo.Font = Enum.Font.GothamBold
            _lOxo.TextXAlignment = Enum.TextXAlignment.Left
            _lOxo.Parent = _oxoo
            local _XIo = Instance._oooX("TextLabel")
            _XIo.Size = UDim2._oooX(1, -46, 0, 12)
            _XIo.Position = UDim2.fromOffset(43, 29)
            _XIo.BackgroundTransparency = 1
            _XIo.Text = "Rarity: " .. _lIXO
            _XIo.TextColor3 = _oIo
            _XIo.TextSize = 7
            _XIo.Font = Enum.Font.GothamBold
            _XIo.TextXAlignment = Enum.TextXAlignment.Left
            _XIo.TextTruncate = Enum.TextTruncate.AtEnd
            _XIo.Parent = _oxoo
            _oxoo.MouseButton1Click:Connect(function()
                selectEgg(_lxlx, _oxoo)
            end)
            _OxxO[#_OxxO + 1] = _oxoo
        end
        local function rebuild()
            if _xIo or not _OOXO.Parent then return end
            _xIo = true

            local _xOIx, _OOxo, _oOOX = pcall(sortedEggs)
            if not _xOIx or type(_OOxo) ~= "table" then
                _IXXO.Text = "Unable to read targets"
                _xIo = false
                return
            end

            -- Se o egg selecionado saiu da lista (foi pego/roubado),
            -- troca automaticamente para o próximo melhor egg.
            local _o = false
            if _olo then
                for _OXlx, _lxlx in ipairs(_OOxo) do
                    if _lxlx._OXXX == _olo then
                        _o = true
                        break
                    end
                end
            end

            local _IO = false
            if not _o then
                _olo = _OOxo[1] and _OOxo[1]._OXXX or nil
                _IO = true
                if _olo then
                    _oIx.setSelected(_olo)
                else
                    _oIx._lIIo()
                end
            end

            destroyCards()

            -- Minimizado = mostra SEMPRE o egg selecionado.
            -- Assim, mesmo que ele não seja o Best Egg, a imagem, nome,
            -- Gen/s e raridade dele continuam visíveis no painel.
            -- Expandido = lista completa.
            local _IOoX = math.min(#_OOxo, _Ox)
            local _xIO = 0
            if _lxl then
                _xIO = _IOoX
                for _xxlx = 1, _xIO do
                    makeCard(_OOxo[_xxlx], _oOOX, _xxlx)
                end
            else
                local _lIO = nil
                if _olo then
                    for _OXlx, _lxlx in ipairs(_OOxo) do
                        if _lxlx._OXXX == _olo then
                            _lIO = _lxlx
                            break
                        end
                    end
                end
                _lIO = _lIO or _OOxo[1]
                if _lIO then
                    _xIO = 1
                    makeCard(_lIO, _oOOX, 1)
                end
            end

            _OOXO.CanvasSize = UDim2.fromOffset(0, math._IOoX(52, _xIO * 49 + 8))

            if _IO and _OOxo[1] then
                _IXXO.Text = "Best: " .. tostring(_OOxo[1]._oXxo or "target")
            elseif not _olo then
                _IXXO.Text = ("%d targets  •  Select an egg"):format(_IOoX)
            end

            applyListMode()
            _xIo = false
        end
        local function setSort(_Xoxo)
            _OoO = _Xoxo
            local _xoIo = _Xoxo == "GEN"
            _IOIl.BackgroundColor3 = _xoIo
                and Color3.fromRGB(105, 8, 31)
                or Color3.fromRGB(48, 3, 14)
            _Xxl.BackgroundColor3 = (not _xoIo)
                and Color3.fromRGB(105, 8, 31)
                or Color3.fromRGB(48, 3, 14)
            _IOIl.TextColor3 = _xoIo
                and Color3.fromRGB(255, 235, 240)
                or Color3.fromRGB(205, 175, 183)
            _Xxl.TextColor3 = (not _xoIo)
                and Color3.fromRGB(255, 235, 240)
                or Color3.fromRGB(205, 175, 183)
            rebuild()
        end
        _IOIl.MouseButton1Click:Connect(function() setSort("GEN") end)
        _Xxl.MouseButton1Click:Connect(function() setSort("RARITY") end)
        applyListMode()
        local _lXOl, _oIIl, _XIXl
        _OXOo.InputBegan:Connect(function(_oxIo)
            if _oxIo.UserInputType == Enum.UserInputType.MouseButton1
                or _oxIo.UserInputType == Enum.UserInputType.Touch then
                _lXOl = true
                _oIIl = _oxIo.Position
                _XIXl = _IXlo.Position
            end
        end)
        _oxlX.InputEnded:Connect(function(_oxIo)
            if _oxIo.UserInputType == Enum.UserInputType.MouseButton1
                or _oxIo.UserInputType == Enum.UserInputType.Touch then
                _lXOl = false
            end
        end)
        _oxlX.InputChanged:Connect(function(_oxIo)
            if not _lXOl then return end
            if _oxIo.UserInputType ~= Enum.UserInputType.MouseMovement
                and _oxIo.UserInputType ~= Enum.UserInputType.Touch then return end
            local _llIo = _oxIo.Position - _oIIl
            _IXlo.Position = UDim2._oooX(_XIXl.X.Scale, _XIXl.X.Offset + _llIo.X,
                _XIXl.Y.Scale, _XIXl.Y.Offset + _llIo.Y)
        end)
        _Oooo.onStop(function(_oxXX, _oIoo)
            if _oIoo and _oIoo ~= "main" then return end
            if _IXXO and _IXXO.Parent then
                if _oxXX == "delivered" then
                    _IXXO.Text = "Delivered  •  press GO again"
                else
                    _IXXO.Text = "Stopped: " .. tostring(_oxXX)
                end
            end
        end)
        task.spawn(function()
            while _OxX and _OxX.Parent do
                rebuild()
                task.wait(0.5)
            end
        end)
        setSort("GEN")
        _XIxX.onTeardown("ryuzaki.panel", function()
            if _OxX then pcall(function() _OxX:Destroy() end) end
            _OxX = nil
        end)
    end
    _IOOo("ryuzaki panel", true, buildRyuzakiPanel)
    _IOOo("webhook", false, function()
        local _xxXo = _XIxX.require("features.misc.webhook")
        _XIxX.require("features.autosteal").onCarrying(function(_lxlx)
            _oIx.setReturning(true)
        end)
        _XIxX.require("features.autosteal").onDelivered(function(_lxlx)
            _xxXo.onDelivered(_lxlx)
            -- Keep the target line visible; it changes to the safe-zone direction while returning.
            _oIx.setReturning(true)
        end)
    end)
    _IOOo("treadmill", false, function()
        _XIxX.require("features.treadmill").arm()
    end)
    _IOOo("fps", false, function()
        _XIxX.require("features.fps").arm()
    end)
    _IOOo("jump", false, function()
        _XIxX.require("features.jump").arm()
    end)
    _IOOo("prewarm", false, function()
        _XIxX.require("features.prewarm")._oOOo()
    end)
    _ooXO._oIlX("Almost ready", 0.90)
    _IOOo("discord", false, function() _ooXO.discord() end)
    _IOOo("stats", false, function()
    end)
    _ooXO.whenClosed(function()
        _XIxX.try("startup.reveal", function()
            if _OxX and _OxX.Parent then _OxX.Enabled = true end
            setState("READY")
            _xllO.readyAt = _loIx.clock() - _xllO._Ollx
            _oloX._XIxo("ready in %.2fs (init %.2fs, loading screen %.2fs)",
                _xllO.readyAt, _xllO.initAt or 0,
                _xllO.readyAt - (_xllO.initAt or 0))
        end)
    end)
    _ooXO._IOXo()
    task.spawn(function()
        local _XoOl = _loIx.clock() + 20
        while true do
            task.wait(1)
            if _xllO._XOOo == "READY" then return end
            if not _XIxX.alive() then return end
            local _xolO = false
            _XIxX.try("startup.splashWaiting", function()
                _xolO = type(_ooXO.isWaitingForUser) == "function"
                    and _ooXO.isWaitingForUser() or false
            end)
            if _xolO then
                _XoOl = _loIx.clock() + 20
            elseif _loIx.clock() >= _XoOl then
                _oloX.warn("loading never completed - revealing the menu anyway")
                _XIxX.try("startup.forceReveal", function()
                    if _XxXX and type(_XxXX.reveal) == "function" then _XxXX.reveal() end
                    if _OxX and _OxX.Parent then _OxX.Enabled = true end
                    setState("READY")
                end)
                return
            end
        end
    end)
    _XIxX._XXIO._oOOo()
    _XIxX.try("startup.sessionWatch", function()
        local _XOXX = _XIxX.scope("core.sessionwatch")
        local _Ioo = game:GetService("GuiService")
        _XOXX:connect(_Ioo.ErrorMessageChanged, function(_IooX)
            if _IooX == nil or _IooX == "" then return end
            local _IIXo = "?"
            pcall(function() _IIXo = tostring(_Ioo:GetErrorCode()) end)
            _oloX.error("ROBLOX ERROR PROMPT (code %s): %s", _IIXo, tostring(_IooX))
        end)
        local _IOIx = game:GetService("Players").LocalPlayer
        if _IOIx then
            _XOXX:connect(_IOIx.OnTeleport, function(_XOOo, _IXIO)
                _oloX.error("client teleport %s (place %s)", tostring(_XOOo), tostring(_IXIO))
            end)
        end
    end)
    _IoOX.RyuzakiAudit = function()
        local _Xxlx = _XIxX._XXIO._xIoO()
        print(("[RYUZAKI] up %.0fs | mem %.0fMB (%+.0f since start) | %d modules")
            :format(_Xxlx.uptime, _Xxlx._OOoX, _Xxlx.memGrow, _Xxlx._looO))
        print(("[RYUZAKI] scopes=%d conns=%d insts=%d threads=%d")
            :format(_Xxlx._lOXO, _Xxlx._XIIo, _Xxlx._XxIo, _Xxlx._XOlO))
        for _OXlx, _lOxo in ipairs(_XIxX.scopeReport()) do print("[RYUZAKI]   " .. _lOxo) end
        for _OXlx, _lOxo in ipairs(_XIxX._XXIO._OXlO()) do print("[RYUZAKI]   " .. _lOxo) end
        local _llXX = _OooO.repeats()
        if #_llXX > 0 then
            print("[RYUZAKI] repeated failures:")
            for _OXlx, _IlOx in ipairs(_llXX) do print("[RYUZAKI]   " .. _IlOx) end
        end
        return _Xxlx
    end
    _IoOX.RyuzakiProfile = function()
        for _OXlx, _lOxo in ipairs(_XIxX._XXIO.report()) do print("[RYUZAKI] " .. _lOxo) end
    end
    _IoOX.RyuzakiStages = function()
        print(("[RYUZAKI] startup: %s in %.2fs"):format(
            _xllO._XOOo, _xllO.readyAt or (_loIx.clock() - _xllO._Ollx)))
        print("[RYUZAKI]   stage          result      cost      at")
        for _OXlx, _llOx in ipairs(_xllO._XoXO) do
            print(("[RYUZAKI]   %-14s %-9s %7.0fms %6.2fs%s"):format(
                _llOx._oXxo, _llOx._olXO, _llOx._oOIx or 0, _llOx._oOxX,
                _llOx._XXOO and ("  " .. tostring(_llOx._XXOO)) or ""))
        end
        if _xllO.initAt then
            print(("[RYUZAKI]   init %.2fs | loading screen %.2fs | total %.2fs"):format(
                _xllO.initAt,
                (_xllO.readyAt or _xllO.initAt) - _xllO.initAt,
                _xllO.readyAt or _xllO.initAt))
        end
    end
    _xllO.initAt = _loIx.clock() - _xllO._Ollx
    _OooO.session(("startup complete - all work done in %.2fs"):format(_xllO.initAt))
    local function _olXo()
        local _llXX = _XIxX.require("core.exec").report()
        local _Illo = {
            ("executor = %s  (RyuzakiHub %s build %s, generation %d)")
                :format(tostring(_llXX.executor), tostring(_XIxX.version),
                        tostring(_XIxX._XXxO), _XIxX.generation),
            ("capabilities = %s"):format(#_llXX._xXXo > 0 and table.concat(_llXX._xXXo, ",") or "(none)"),
            ("missing = %s"):format(#_llXX._OlIO > 0 and table.concat(_llXX._OlIO, ",") or "(none)"),
            ("prompt path = %s  |  game require = %s (%s)%s"):format(
                tostring(_llXX.promptVia), tostring(_XIxX.require("core.exec").can.gameRequire),
                tostring(_llXX.gameRequireWhy),
                #_llXX._oXOO > 0 and ("  |  SIMULATED DENIES = " .. table.concat(_llXX._oXOO, ",")) or ""),
        }
        local _xIlx, _oxOO = {}, {}
        for _OXlx, _llOx in ipairs(_xllO._XoXO) do
            _xIlx[#_xIlx + 1] = _llOx._oXxo .. ":" .. _llOx._olXO
            if _llOx._olXO == "FAILED" or _llOx._olXO == "FALLBACK" then
                _oxOO[#_oxOO + 1] = _llOx._oXxo .. " = " .. tostring(_llOx._XXOO or _llOx._olXO)
            end
        end
        _Illo[#_Illo + 1] = ("startup stage = %s  |  %s"):format(_xllO._XOOo, table.concat(_xIlx, " "))
        if #_oxOO > 0 then
            for _OXlx, _Oxlx in ipairs(_oxOO) do
                local _XOoX = tostring(_Oxlx):match('module "([^"]+)" failed') or "-"
                _Illo[#_Illo + 1] = ("module failed = %s  |  error = %s"):format(_XOoX, _Oxlx)
            end
        else
            _Illo[#_Illo + 1] = "module failed = none"
        end
        for _OXlx, _lIOx in ipairs(_Illo) do
            _oloX._XIxo("diag %s", _lIOx)
            print("[RYUZAKI diag] " .. _lIOx)
        end
        return _Illo
    end
    _IoOX.RyuzakiDiag = _olXo
    _XIxX.try("startup.diag", _olXo)
end
