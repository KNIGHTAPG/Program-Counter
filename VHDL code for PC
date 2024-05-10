--4bit PC using VHDL

-----------------------------------
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity buttonCounter is
    Port (
        clk       : in STD_LOGIC;
        btnC      : in STD_LOGIC;
        reset_btn : in STD_LOGIC;
        load_btn  : in STD_LOGIC;
        data_in   : in STD_LOGIC_VECTOR(15 downto 0);
        seg       : out STD_LOGIC_VECTOR(7 downto 0);
        an        : out STD_LOGIC_VECTOR(3 downto 0)
    );
end entity buttonCounter;

architecture Behavioral of buttonCounter is

component debounce
        port (
            clk       : in STD_LOGIC;
            btn       : in STD_LOGIC;
            btn_clr   : out STD_LOGIC
        );
    end component debounce;

component decoder_7seg is
    Port (
           in1   : in STD_LOGIC_VECTOR(15 downto 0);
           out1  : out STD_LOGIC_VECTOR(7 downto 0)
    );
    end component decoder_7seg;

    signal btn_clr : STD_LOGIC;
    signal prevbtn : STD_LOGIC;
    signal counter : STD_LOGIC_VECTOR(15 downto 0) := (others => '0');
    signal stored_value : STD_LOGIC_VECTOR(15 downto 0) := (others => '0');
    signal data_out : STD_LOGIC_VECTOR(3 downto 0);


begin
        d1 : debounce
        port map (
            clk      => clk,
            btn      => btnC,
            btn_clr  => btn_clr
        );
        
    s1 :  decoder_7seg port map (in1 => counter , out1 =>seg);

    process(clk)
    begin
        if rising_edge(clk) then
            an <= "1110";

            if reset_btn = '1' then
                counter <= (others => '0');
            elsif load_btn = '1' then
                counter <= data_in;
            else
                if btn_clr /= prevbtn and btn_clr = '1' then
                    counter <= counter + 1;
                    if counter = "00001111" then
                        counter <= (others => '0');
                    end if;
                end if;
            end if;

            prevbtn <= btn_clr;
        end if;
    end process;

end architecture Behavioral;


--------------------------------------------------------


library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity debounce is
    Port (
        clk       : in STD_LOGIC;
        btn       : in STD_LOGIC;
        btn_clr   : out STD_LOGIC
    );
end entity debounce;

architecture Behavioral of debounce is
    constant delay : integer := 650000; -- 6.5 ms delay
    signal count : integer := 0;
    signal xnew : STD_LOGIC := '0';
begin
    process(clk)
    begin
        if rising_edge(clk) then
            if btn /= xnew then
                count <= 0;
                xnew <= btn;
            elsif count = delay then
                btn_clr <= xnew;
            else
                count <= count + 1;
            end if;
        end if;
    end process;
end architecture Behavioral;


-----------------------------------------------------------------------------

library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.STD_LOGIC_ARITH.ALL;
use IEEE.STD_LOGIC_UNSIGNED.ALL;

entity decoder_7seg is
    Port (
        in1   : in STD_LOGIC_VECTOR(15 downto 0);
        out1  : out STD_LOGIC_VECTOR(7 downto 0)
    );
end entity decoder_7seg;

architecture Behavioral of decoder_7seg is
begin
    process(in1)
    begin
        case in1(3 downto 0) is
            when "0000" =>
                out1 <= "11000000";  -- 0
            when "0001" =>
                out1 <= "11111001";  -- 1
            when "0010" =>
                out1 <= "10100100";  -- 2
            when "0011" =>
                out1 <= "10110000";  -- 3
            when "0100" =>
                out1 <= "10011001";  -- 4
            when "0101" =>
                out1 <= "10010010";  -- 5
            when "0110" =>
                out1 <= "10000010";  -- 6
            when "0111" =>
                out1 <= "11111000";  -- 7
            when "1000" =>
                out1 <= "10000000";  -- 8
            when "1001" =>
                out1 <= "10011000";  -- 9
            when "1010" =>
                out1 <= "10001000";  -- A
            when "1011" =>
                out1 <= "10000011";  -- B
            when "1100" =>
                out1 <= "11000110";  -- C
            when "1101" =>
                out1 <= "10100001";  -- D
            when "1110" =>
                out1 <= "10000110";  -- E
            when "1111" =>
                out1 <= "10001110";  -- F
            when others =>
                out1 <= (others => '0');  -- Default case
        end case;
    end process;
end architecture Behavioral;
