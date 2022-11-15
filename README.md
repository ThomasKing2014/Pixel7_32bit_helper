# Pixel 7 32-bit mode helper

## Introduction

According to this post - [Pixel 7, the first 64-bit-only Android phone](https://android-developers.googleblog.com/2022/10/64-bit-only-devices.html), Pixel 7 and Pixel 7 Pro are the first Android phones to support only 64-bit apps. This truth is that all the 32-bit dynamic libraries are built, and it's nothing different with Pixel 6. That means Pixel 7 can support 32-bit apps. The only step is to turn the related switch on.

    Use the custom Magisk to patch the stock init_boot image. You can follow those [steps](https://www.xda-developers.com/how-to-unlock-bootloader-root-magisk-google-pixel-7-pro).

After rebooting, the zygote 32-bit process can be found. Now you can install the 32-bit-only apps!

    panther:/data/local/tmp $ ps -ef |grep zygote
    root           979     1 0 17:45:52 ?     00:00:02 zygote64
    root          1066     1 0 17:45:53 ?     00:00:01 zygote
    webview_zygote 1980  979 0 17:45:57 ?     00:00:00 webview_zygote
    shell         9453  9447 36 20:53:25 pts/0 00:00:00 grep zygote

As the project is experimental, I do not try to solve other issues. 

## Details

The switch is "ro.zygote" property. To spawn the zygote 32-bit process, it requires setting the value to "ro.zygote=zygote64_32". And it also requires adding the 32-bit abi to both "ro.vendor.product.cpu.abilist" and "ro.vendor.product.cpu.abilist32" properties.

The diff files are for [Magisk](https://github.com/topjohnwu/Magisk).

`magisk-25200-zygote64_32.diff` is for v25.2  
`magisk-24300-zygote64_32.diff` is for v24.3

## License

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.
