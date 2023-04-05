console.log("Youtube Multi Downloader Online");
"youtubemultidownloader.com" != location.hostname && "youtubemultidownloader.net" != location.hostname && "www.youtubemultidownloader.net" != location.hostname && "youtube1s.com" != location.hostname && "www.youtubemultidownloader.com" != location.hostname && "youtube1s.com" != location.hostname && (location.href = "https://youtubemultidownloader.net");
$(document).ready(function () {
    initControl()
});
var listQuality = {
    22: {format: "MP4", quality: "720P", audio: !0},
    18: {format: "MP4", quality: "360P", audio: !0},
    138: {format: "MP4 No Audio", quality: "8K", audio: !1},
    266: {format: "MP4 No Audio", quality: "4K", audio: !1},
    264: {format: "MP4 No Audio", quality: "2K", audio: !1},
    137: {format: "MP4 No Audio", quality: "1080P", audio: !1},
    136: {format: "MP4 No Audio", quality: "720P", audio: !1},
    135: {format: "MP4 No Audio", quality: "480P", audio: !1},
    134: {format: "MP4 No Audio", quality: "360P", audio: !1},
    133: {format: "MP4 No Audio", quality: "240P", audio: !1},
    160: {format: "MP4 No Audio", quality: "144P", audio: !1},
    140: {format: "Audio", quality: "128kb/s M4A", audio: !0},
    141: {format: "Audio", quality: "256kb/s M4A", audio: !0},
    36: {format: "3GP", quality: "240P", audio: !0},
    17: {format: "3GP", quality: "144P", audio: !0},
    43: {format: "WebM No Audio", quality: "360P", audio: !1},
    313: {format: "WebM No Audio", quality: "4K", audio: !1},
    271: {format: "WebM No Audio", quality: "2K", audio: !1},
    248: {format: "WebM No Audio", quality: "1080P", audio: !1},
    247: {format: "WebM No Audio", quality: "720P", audio: !1},
    244: {format: "WebM No Audio", quality: "480P", audio: !1},
    243: {format: "WebM No Audio", quality: "360P", audio: !1},
    242: {format: "WebM No Audio", quality: "240P", audio: !1},
    278: {format: "WebM No Audio", quality: "144P", audio: !1}
};
jQuery.xhrPool = [];
jQuery.xhrPool.abortAll = function () {
    var a = [], c;
    for (c in this) !0 === isFinite(c) && a.push(this[c]);
    for (c in a) a[c].abort()
};
jQuery.xhrPool.remove = function (a) {
    for (var c in this) if (this[c] === a) {
        jQuery.xhrPool.splice(c, 1);
        break
    }
};
$(document).ajaxSend(function (a, c, b) {
    jQuery.xhrPool.push(c)
});
$(document).ajaxComplete(function (a, c, b) {
    jQuery.xhrPool.remove(c)
});
String.prototype.format || (String.prototype.format = function () {
    var a = arguments;
    return this.replace(/{(\d+)}/g, function (c, b) {
        return "undefined" != typeof a[b] ? a[b] : c
    })
});
Object.defineProperty(Object.prototype, "length", {
    get: function () {
        return Object.keys(this).length
    }
});
var listConvert = {
    138: {format: "MP4", quality: "8K", audio: !0},
    266: {format: "MP4", quality: "4K", audio: !0},
    264: {format: "MP4", quality: "2K", audio: !0},
    137: {format: "MP4", quality: "1080P", audio: !0},
    135: {format: "MP4", quality: "480P", audio: !0},
    18: {format: "MP4", quality: "360P", audio: !0},
    140: {format: "Audio", quality: "MP3 320Kbps", audio: !0},
    141: {format: "Audio", quality: "MP3 320Kbps", audio: !0}
}, isHomeBusy = !1;

function initControl() {
    $("#inputUrl").on("input", function () {
        if (!isHomeBusy) {
            var a = getYoutubeID($("#inputUrl").val());
            a ? Home_DownloadVideo(a) : ($("#lbError").show(500), $("#lbError").text("Oops, wrong youtube link!"), $("#Loading").hide())
        }
    });
    $("#convertBack").unbind("click").bind("click", function () {
        $("#Convert .alert").hide();
        $("#Convert").hide();
        $("#Download").show();
        $("#inputUrl").attr("readonly", !1)
    });
    $("#txtDownload").on("click", function () {
        this.select()
    });
    $("#btnDownloadVideo").on("click", function () {
        $("#inputUrl").trigger("input")
    });
    $("#inputPlaylist").on("input", function () {
        $("#lbError").hide();
        getPlaylistID($("#inputPlaylist").val()) ? ($("#lbError").hide(500), $("#Download").html('<table class="table" id="ListVideo"> <thead> <tr> <th>#</th> <th>Image</th> <th>Title</th> <th>Download</th> </tr> </thead> <tbody> </tbody> </table>'), Playlist_GetListVideo($("#inputPlaylist").val(), ""), $("#txtDownload").val("")) : ($("#lbError").show(500), $("#lbError").text("Oops, wrong playlist link!"), $("#Loading").hide())
    });
    $("#inputChannel").on("input", function () {
        var a = $("#inputChannel").val();
        -1 !== a.indexOf("youtube.com/c/") || -1 !== a.indexOf("youtube.com/@") || -1 !== a.indexOf("youtube.com/user") || -1 !== a.indexOf("youtube.com/channel") ? Playlist_GetListVideo(a, "") : ($("#lbError").show(500), $("#lbError").text("Oops, wrong channel link!"))
    });
    $("#cbQuality").change(function () {
        localStorage.setItem("quality", $("#cbQuality option:selected").val())
    });
    $("#chkAutoQuality").change(function () {
        localStorage.setItem("autoQuality", $("#chkAutoQuality").prop("checked"))
    });
    $("#chkAutoOrder").change(function () {
        localStorage.setItem("autoOrder", $("#chkAutoOrder").prop("checked"))
    });
    localStorage.getItem("quality") && $("#cbQuality").val(localStorage.getItem("quality"));
    "false" == localStorage.getItem("autoQuality") ? $("#chkAutoQuality").prop("checked", !1) : $("#chkAutoQuality").prop("checked", !0);
    "false" == localStorage.getItem("autoOrder") ? $("#chkAutoOrder").prop("checked", !1) : $("#chkAutoOrder").prop("checked", !0);

    if (getParameterByName("url")){
        if (getParameterByName("url").includes("channel")){
            if (!location.pathname.includes("channel")) location.href ="/channel.html?url=" + encodeURI(getParameterByName("url"))
            else{
                $("#inputChannel").val(getParameterByName("url"));
                $("#inputChannel").trigger("input");
            }
        }else {
            $("#inputUrl").val(getParameterByName("url"));
            $("#inputUrl").trigger("input");
        }

    }

}

var playlistIndex = 0, playlistTotalVideo = 1;

function Playlist_GetListVideo(a, c) {
    if (!reachLimit) {
        var b;
        c || ($.xhrPool.abortAll(), $("#ListVideo tbody").html(""), playlistIndex = 0);
        $("[name='btnLoadMore']").attr("disabled", !0);
        API_SERVER ? $.ajax({
            type: "GET", url: API_SERVER + "/playlist", data: {url: a, nextPageToken: c}, beforeSend: function () {
                $(".spinner").show();
                $("#lbError").hide()
            }, success: function (d) {
                if (d.status) {
                    $(".spinner").hide();
                    playlistTotalVideo = d.totalResults;
                    b = d.nextPageToken;
                    for (var f = 0; f < d.items.length; f++) {
                        var e = d.items[f].id, g = d.items[f].title,
                            h = "https://img.youtube.com/vi/" + e + "/default.jpg";
                        $("#Loading").hide();
                        g = '<tr><th scope="row">' + (playlistIndex + 1) + '</th><td><img style="height: 55px;width: 90px;" src="' + h + '"></td><td>' + g + '</td><td><div id="Download-' + e + '"><div class="progress"> <div class="progress-bar progress-bar-striped active" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%"> <span class="sr-only"></span></div> </div></div></div></td></tr>';
                        $("#ListVideo tbody").append(g);
                        Playlist_DownloadVideo(e);
                        playlistIndex++;
                        $("[name='btnLoadMore']").removeAttr("disabled");
                        $("[name='btnLoadMore']").text("Load more videos (" + (playlistTotalVideo - playlistIndex) + " left)")
                    }
                    b ? ($("[name='btnLoadMore']").show(), $("[name='btnLoadMore']").unbind("click").bind("click", function () {
                        Playlist_GetListVideo(a, b)
                    })) : ($("[name='btnLoadMore']").hide(), $("#Loading").hide())
                } else swal.fire({
                    title: "Error",
                    text: "Oops, there is something wrong with server. Do you want to try again?",
                    type: "warning",
                    showCancelButton: !0,
                    confirmButtonColor: "#3085d6",
                    cancelButtonColor: "#d33",
                    confirmButtonText: "Yes, try again!",
                    allowOutsideClick: !1
                }).then(function (b) {
                    b.value && Playlist_GetListVideo(a, c)
                })["catch"](function () {
                    $("#lbError").text("Error: Stopped dua server error, please report this error.");
                    $("#Loading").hide();
                    $("#lbError").show()
                })
            }, error: function (b) {
                swal.fire({
                    title: "Error",
                    text: "Oops, there is something wrong with connection, maybe server too busy. Do you want to try again?",
                    type: "warning",
                    showCancelButton: !0,
                    confirmButtonColor: "#3085d6",
                    cancelButtonColor: "#d33",
                    confirmButtonText: "Yes, try again!",
                    allowOutsideClick: !1
                }).then(function (b) {
                    b.value && Playlist_GetListVideo(a, c)
                })["catch"](function () {
                    $("#lbError").text("Error: Stopped dua connection problem, maybe server too busy.");
                    $("#Loading").hide();
                    $("#lbError").show()
                })
            }, complete: function () {
                $(".spinner").hide()
            }, dataType: "json"
        }) : swal.fire({
            title: "Error",
            text: "Oops, service unavailable or something goes wrong with server.",
            type: "warning",
            showCancelButton: !0,
            confirmButtonColor: "#3085d6",
            cancelButtonColor: "#d33",
            confirmButtonText: "Yes, try again!",
            allowOutsideClick: !1
        }).then(function () {
        })
    }
}

var reachLimit = !1, listRetry = {}, listDownload = {};

function removeURLParameter(a, c) {
    var b = a.split("?");
    if (2 <= b.length) {
        for (var d = encodeURIComponent(c) + "=", f = b[1].split(/[&;]/g), e = f.length; 0 < e--;) -1 !== f[e].lastIndexOf(d, 0) && f.splice(e, 1);
        a = b[0] + "?" + f.join("&")
    }
    return a
}

function Playlist_DownloadVideo(a) {
    if (reachLimit) $("#Download-" + a).html('<span class="badge badge-danger">Usage limit</span>'); else {
        var c = parseInt($("#cbQuality").find("option:selected").val()), b, d = c, f = !1;
        $.ajax({
            type: "GET",
            url: API_SERVER + "/video",
            data: {url: "https://www.youtube.com/watch?v=" + a},
            beforeSend: function () {
            },
            success: function (e) {
                if (e.status) if (-1 < e.title.indexOf("Official Music Video") || e.copyright && 0 < e.copyright.length) $("#Download-" + a).parent().parent().find("img").attr("src", "https://img.youtube.com/vi/z/default.jpg"), $("#Download-" + a).html('<span class="badge badge-danger">This video has been blocked on copyright grounds</span>'), sessionStorage.getItem("notify") || (sessionStorage.setItem("notify", !0), Swal.fire({
                    title: "Copyright Material Detected!",
                    text: "As our new ToS, you can't download videos that contains copyright song. If this is your video and have full right and permission, you can try YoutubePlaylist backup service which allow backup all videos from your account.",
                    type: "warning",
                    showCancelButton: !0,
                    confirmButtonColor: "#3085d6",
                    cancelButtonColor: "#d33",
                    confirmButtonText: "Yes, try it!"
                }).then(function (a) {
                    a.value && document.getElementById("try_from_playlist").click()
                })); else {
                    e.title = e.title.replace('"', "'");
                    e.title = e.title.replace('"', "'");
                    e.title = encodeURIComponent(e.title);
                    var g = $("#Download-" + a).parent().parent().find("th[scope]").html();
                    10 > g && (g = "0" + g);
                    g += ".";
                    $("#chkAutoOrder").prop("checked") || (g = "");
                    if ($("#chkAutoQuality").prop("checked")) {
                        for ("undefined" !== typeof e.format.find(function (a) {
                            return a.id == d
                        }) && (b = removeURLParameter(e.format.find(function (a) {
                            return a.id == d
                        }).url, "title") + "&title=" + g + e.title + getExt(d)); !b && (d = autoQuality(d), "undefined" !== typeof e.format.find(function (a) {
                            return a.id == d
                        }) && (b = removeURLParameter(e.format.find(function (a) {
                            return a.id == d
                        }).url, "title") + "&title=" + g + e.title + getExt(d)), d);) ;
                        d != c && (f = !0)
                    } else "undefined" !== typeof e.format.find(function (a) {
                        return a.id == d
                    }) && (b = removeURLParameter(e.format.find(function (a) {
                        return a.id == d
                    }).url, "title") + "&title=" + g + e.title + getExt(d));
                    !b || -1 < b.indexOf("/videoplayback/") ? $("#Download-" + a).html('<span class="badge badge-danger">Not Found!</span>') : (e = $("#cbQuality option[value=" + d + "]").text(), f ? $("#Download-" + a).html('<a download href="' + b + '" class="btn btn-outline-secondary" role="button"><span class="glyphicon glyphicon-sort-by-attributes-alt"></span>' + e + "</a> ") : $("#Download-" + a).html('<a download href="' + b + '" class="btn btn-outline-secondary" role="button">' + e + "</a> "), $("#txtDownload").val($("#txtDownload").val() + b + "\n"), $("#Download-" + a).attr("link", b), listDownload[a] = b)
                } else {
                    if (-1 < e.message.indexOf("limit")) {
                        $("#Download-" + a).html('<span class="badge badge-danger">Usage limit</span>');
                        showReachLimit();
                        return
                    }
                    $("#Download-" + a).html('<span class="badge badge-danger">' + e.message + "</span>")
                }
                e = (listDownload.length / playlistTotalVideo * 100).toFixed(0);
                $("#lbStatus").css("width", e + "%");
                $("#lbStatus").text(e + "% (" + listDownload.length + "/" + playlistTotalVideo + ") video(s) available to download")
            },
            error: function (b) {
                listRetry[a] || (listRetry[a] = 0);
                listRetry[a] += 1;
                if (3 < listRetry) $.notify({message: "Oops, the video id <b>{0}</b> can't download after 3 times retry".format(a)}, {type: "danger"}); else return Playlist_DownloadVideo(a)
            },
            complete: function () {
            },
            dataType: "json"
        })
    }
}

function showReachLimit() {
    reachLimit || (swal.fire({
        title: "Usage limit",
        text: "Oops, you has reach the limit of usage per day. If you want to download large number video please consider upgrade to donation plan (coming soon) or wait next day",
        type: "warning",
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Okey I got it!",
        allowOutsideClick: !1
    }).then(function () {
    })["catch"](function () {
    }), reachLimit = !0)
}

function Home_DownloadVideo(a) {
    $.xhrPool.abortAll();
    API_SERVER ? $.ajax({
        type: "GET",
        url: API_SERVER + "/video",
        data: {url: "https://www.youtube.com/watch?v=" + a},
        beforeSend: function () {
            isHomeBusy = !0;
            $("#Loading").show();
            $("#Convert .alert").hide();
            $("#Convert").hide();
            $("#Download").hide();
            $("#lbError").hide();
            $("#Download_Quality div[format]").html("")
        },
        success: function (c) {
            c.status ? -1 < c.title.indexOf("Official Music Video") || c.copyright && 0 < c.copyright.length ? ($("#Download_Error").show(), $("#Download_Quality").hide(), $("#Download_Image h6").text(c.title), $("#Download_Image .thumbnail img").attr("src", "https://img.youtube.com/vi/z/default.jpg"), $("#btnBackup").html('<a target="_blank" rel="noreferrer"  role="button" class="btn btn-outline-primary" href="https://youtubeplaylist.cc" style="min-width: 140px;">Try it now!</a>'), $("#Download").show()) : ($("#Download_Image img").attr("src", "https://img.youtube.com/vi/" + a + "/hqdefault.jpg"), $("#Download_Error").hide(), $("#Download_Quality").show(), $("#Download_Image h6").text(c.title), c.format.forEach(function (b) {
                if (b.id && 0 > b.url.indexOf("yt_otf")) {
                    var d = b.url;
                    itag = b.id;
                    if (listConvert[itag]) {
                        var f = listQuality[itag];
                        b = b.size;
                        $("#Download_Quality div[format='" + listConvert[itag].format + "']").append('<a  target="_blank" rel="noreferrer"   quality="' + f.quality + '" role="button" class="btn btn-success" href="https://youtubeplaylist.cc/?url=https://www.youtube.com/watch?v=' + a + '&source=button" videoId="' + a + '" style=" min-width: 140px; ">' + f.quality + " (" + formatBytes(b) + ")</a>");
                        $("#Download_Quality div[format='" +
                            listConvert[itag].format + "']").parent(".panel").show()
                    } else if (listQuality[itag]) {
                        f = listQuality[itag];
                        b = b.size;
                        var e = "";
                        var g = "btn btn-outline-secondary";
                        f.audio ? g = "btn btn-primary" : e = '<span class="glyphicon glyphicon-volume-off"></span>';
                        $("#Download_Quality div[format='" + f.format + "']").parent(".panel").show();
                        $("#Download_Quality div[format='" + f.format + "']").append('<a  target="_blank" rel="noreferrer"   quality="' + f.quality + '" download="' + encodeURIComponent(c.title) + getExt(itag) + '" role="button" class="' +
                            g + '" href="' + d + "&title=" + encodeURIComponent(c.title) + getExt(itag) + '" style=" min-width: 140px; ">' + f.quality + " (" + formatBytes(b) + ")" + e + "</a>")
                    }
                }
            }), c.subtitle && $.each(c.subtitle, function (b, c) {
                setTimeout(function () {
                    $("#Download_Quality div[format='Subtitle']").append('<a href="{0}" class="btn btn-info" role="button">{1}</a>'.format(API_SERVER + "/subtitle?url=https://www.youtube.com/watch?v=" + a + "&lang=" + b, c));
                    $("#Download_Quality div[format='Subtitle']").parent(".panel").show()
                }, 0)
            }), $("div.panel-body[format]").each(function () {
                $(this).html($(this).children("a[quality]").sort(function (a, c) {
                    return parseInt($(a).attr("quality")) < parseInt($(c).attr("quality")) ? 1 : -1
                }))
            }), $("#Download").show(), $("div[format='MP4']").append('  <a target="_blank" rel="noreferrer"  role="button" class="btn btn-primary" href="https://youtubeplaylist.cc/?url=https://www.youtube.com/watch?v=' + a + '&source=button" style="min-width: 140px;">480P</a>'), $("div[format='Audio']").append('  <a target="_blank" rel="noreferrer"  role="button" class="btn btn-primary" href="https://youtubeplaylist.cc?url=https://www.youtube.com/watch?v=' +
                a + '&source=button" style="min-width: 140px;">MP3 320kb/s</a>')) : ($("#lbError").html("Error: " + c.message), $("#lbError").show(), $("#Download").hide())
        },
        error: function (c, b) {
            $("#Download").hide();
            swal.fire({
                title: "Error",
                text: "Oops, there is something wrong with connection, maybe server is too busy or your IP is banned. Do you want to try again?",
                type: "warning",
                showCancelButton: !0,
                confirmButtonColor: "#3085d6",
                cancelButtonColor: "#d33",
                confirmButtonText: "Yes, try again!",
                allowOutsideClick: !1
            }).then(function (b) {
                b.value && Home_DownloadVideo(a)
            });
            $("#Loading").hide();
            $("#inputUrl").val("")
        },
        complete: function () {
            $("#Loading").hide();
            $("#inputUrl").val("");
            isHomeBusy = !1
        },
        dataType: "json"
    }) : swal.fire({
        title: "Error",
        text: "Oops, service unavailable or something goes wrong with server.",
        type: "warning",
        showCancelButton: !0,
        confirmButtonColor: "#3085d6",
        cancelButtonColor: "#d33",
        confirmButtonText: "Yes, try again!",
        allowOutsideClick: !1
    }).then(function () {
    })
}



function getParameterByName(a, c) {
    c || (c = window.location.href);
    a = a.replace(/[\[\]]/g, "\\$&");
    var b = (new RegExp("[?&]" + a + "(=([^&#]*)|&|#|$)")).exec(c);
    return b ? b[2] ? decodeURIComponent(b[2].replace(/\+/g, " ")) : "" : null
}

function autoQuality(a) {
    var c = [22, 18], b = [43, 313, 271, 248, 247, 244, 243, 242, 278], d = [36, 17], f = [141, 140];
    if (0 !== c.indexOf(a) + 1) return c[c.indexOf(a) + 1];
    if (0 !== b.indexOf(a) + 1) return b[b.indexOf(a) + 1];
    if (0 !== d.indexOf(a) + 1) return d[d.indexOf(a) + 1];
    if (0 !== f.indexOf(a) + 1) return f[f.indexOf(a) + 1]
}

function getExt(a) {
    return ""
}

function getYoutubeID(a) {
    return (a = a.match(/^.*((youtu.be\/)|(v\/)|(\/u\/\w\/)|(embed\/)|(watch\?))\??v?=?([^#&\?]*).*/)) && 11 == a[7].length ? a[7] : !1
}

function getPlaylistID(a) {
    if ((a = /[&?]list=([a-z0-9_-]+)/i.exec(a)) && 0 < a[1].length) return a[1]
}

function formatBytes(a, c) {
    var b = c ? 1E3 : 1024;
    if (Math.abs(a) < b) return a + " B";
    var d = c ? "kB MB GB TB PB EB ZB YB".split(" ") : "KiB MiB GiB TiB PiB EiB ZiB YiB".split(" "), f = -1;
    do a /= b, ++f; while (Math.abs(a) >= b && f < d.length - 1);
    return a.toFixed(1) + " " + d[f]
}

function getQueryParams(a) {
    a = a.split("+").join(" ");
    for (var c = {}, b, d = /[?&]?([^=]+)=([^&]*)/g; b = d.exec(a);) c[decodeURIComponent(b[1])] = decodeURIComponent(b[2]);
    return c
}

var oldbeforeunload = window.onbeforeunload;
window.onbeforeunload = function () {
    var a = oldbeforeunload ? oldbeforeunload() : void 0;
    void 0 == a && $.xhrPool.abortAll();
    return a
};
